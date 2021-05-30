---
title: "Euler axis solution space for mapping kinematic chains: A modified inverse kinematics approach"
#date: 2021-04-04
categories:
  - blog

tags:
  - Kinematics
  - Inverse Kinematics
  - Linear Algebra
  - Rotations

---

### Background
Generally, a kinematic chain can be described as a hierarchical system of links and joints. Kinematic chains are described by 1) the locations and orientations of each of the joints, and 2) the heirarchy of the joints in the system, e.g. using a directed graph. Inverse kinematics is an approach used to reorient an open kinematic chain (i.e. no looping) to achieve a desidered location and orientation for the final joint in the chain (referred to as the end-effector in robotics). This problem can be solved either analytically or numerically depending on the complexity of the chain, i.e. the Degrees of freedom of the system. If the degrees of freedom of the chain exceeds the degrees of freedom of the end-effector then there exists an infinite number of solutions, and numerical optimization should be used. In this post I develop a method for mapping one kinematic chain (a) to another (b), where the latter does not contain any information on joint orientations. Where the chains must have the same number of joints and the same joint heirarchy, but may have differing and dsproportional link lengths. This is distict from traditional forms of inverse kinematics, in that the target involves mapping vectors throughout the chain, and does not specify degrees of freedom in terms of joint locations nor orientations.

ADD A FIGURE FOR THE MAPPED COMPLEX KINEMATIC CHAIN

In a previous post, I described how in SO(3) an infinite number of rotation matrices, or Euler/Screw axis-angle combinations can be applied to map one vector (a) onto another vector (b). However, the solution space is constrained such that the Euler/Screw axis must lay on the plane that bisects the vectors.

> For more infor see my blog post:
> ['Non-uniqueness of the Euler axis in vector mapping'](https://kevgildea.github.io/blog/Euler-Axis-Vector-Mapping/)


### Euler axis solution space for mapping kinematic chains
If we assign an initial local coordinate system to vector a, for example, if we set choose it to be aligned with the global coordinate system then we can see the Euler axis solution space for reorientation of this local coordinate system. 

<p align="center">
  <img src="/assets/images/Optimized-Inverse-Kinematics/fig1.gif" width="700">
</p>

Alternatively, we can choose a simpler example, with an initial local coordinate system for vector a where the Y axis (green) is alligned with the vector. In this case, the solution space is more easily visualised. 

<p align="center">
  <img src="/assets/images/Optimized-Inverse-Kinematics/fig2.gif" width="700">
</p>

We would like to extend this method to a kinematic chain, which will require an iterative calculation of the Euler axis solution space for each joint throughout the chain.

Firstly, we can define a simple open kinematic chain a. We express chain a using... joint orientations and positions relative to their parent joints, and for the root node.. (See 4B17 notes and Wittenburg).. We can apply forward kinematics to bring calculate the joint positions and orientations in the global coordinate system.

Implementation of forward kinematics:

```python
def FK_local2global(chain,dir_graph): 
    """ perform forward kinematics to to convert joint orientations and position vectors into the global coordinate system"""
    ref_space_ori = np.array([[1, 0, 0],
                              [0, 1, 0],
                              [0, 0, 1]])
    ref_space_pos = np.array([0, 0, 0])
    oris=[]
    poss=[]
    for i in range (len(chain)):
        path = jnt_path(dir_graph, 0, i)
        ori = ref_space_ori
        pos = ref_space_pos
        for j in path:
            pos=pos + ori @ chain[j][2]
            ori=ori @ chain[j][1]
        oris.append(ori)
        poss.append(pos)
    
    return oris, poss
```

We can then define chain b using only joint positions in the global coordinate system, and the same directed graph as chain a.

PLOT OF SIMPLE CHAINS A AND B

MATHEMATICALLY DESCRIBE 'def IK_simple_open_chain'

Implementation of a modified inverse kinematics approach for mapping a simple kinematic chain:

```python
def IK_simple_open_chain(chain_a,chain_b,dir_graph): # Consider renaming Could more aptly be described as a modified forward kinematics approach?
    """ perform inverse kinematics to map a simple kinematic chain a (an open chain without forking) to chain b, which must have the same directed graph"""
    ori_a, pos_a = FK_local2global(chain_a,dir_graph)
    _, pos_b = FK_local2global(chain_b,dir_graph)

    pos_a= pos_a - chain_a[0][2]
    pos_b= pos_b - chain_b[0][2]
    
    #convert directed graph for use in nx
    dir_graph = nx.DiGraph(dir_graph)

    repos_a_EAS=[]
    reori_a_EAS=[]
    Euler_axis=[]
    Euler_axes=[]

    for i in range(1,360,1): 
        reori_a=copy.deepcopy(ori_a)
        repos_a=copy.deepcopy(pos_a)
        Euler_axis=[]
        for j in range(len(chain_a)):
            downchain = list(nx.nodes(nx.dfs_tree(dir_graph, j))) # list of index values for j and all joints down chain #CREATE MY OWN FN. FOR THIS?
            if j < len(chain_a)-1:
                ROTM= Vector_mapping_Euler_Axis_Space(repos_a[j+1]-repos_a[j], pos_b[j+1]-pos_b[j])[2][i]
                Euler_axis.append(Vector_mapping_Euler_Axis_Space(repos_a[j+1]-repos_a[j], pos_b[j+1]-pos_b[j])[0][i])
            for k in range(len(downchain)):
                if downchain[0] != downchain[-1]:
                    reori_a[downchain[k]]= ROTM @ reori_a[downchain[k]]
                if downchain[k] != downchain[-1]:
                    repos_a[downchain[k+1]]= repos_a[j] + ROTM @ (repos_a[downchain[k+1]]-repos_a[j])
        repos_a= repos_a + chain_a[0][2]

        repos_a_EAS.append(repos_a)
        reori_a_EAS.append(reori_a)
        Euler_axes.append(Euler_axis)

    return reori_a_EAS, repos_a_EAS, Euler_axes
```

PLOT EXAMPLE OF THE SOLUTION SPACE FOR 'def IK_simple_open_chain'

DESCRIBE THE MATHEMATICS OF EXTENDING THIS TO A COMPLEX KINEMATIC CHAIN

Implementation of a modified inverse kinematics approach for mapping a complex kinematic chain:

```python
def IK_complex_open_chain(chain_a, chain_b,dir_graph): 
    """ perform inverse kinematics to map a complex kinematic chain a (an open chain with forking) to chain b, which must have the same directed graph"""


    return 

```

### Implications
