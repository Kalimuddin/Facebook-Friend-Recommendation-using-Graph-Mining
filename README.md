# Facebook-Friend-Recommendation-using-Graph-Mining

## Problem Definition and Data Requirements :
- Problem Statement is to predict missing links in a given directed social graph for friends/followers recommendation.
- Main aim is to predict the probability score of a link so as to recommend the "higest probability links" to a user.
- Achieved best F1 Score = 0.924, The most important part of this case study is Featurization.
- Required Data available at : https://drive.google.com/drive/folders/1HrxehE9wrSaHcaXzRrUE0cqo5czx3kEk?usp=sharing

## EDA : 
- Basic Infromation :
  - Type: DiGraph
  - Number of nodes: 1862220
  - Number of edges: 9437519
  - Average in degree:   5.0679
  - Average out degree:   5.0679

- Displaying a sub graph :
![1](https://user-images.githubusercontent.com/54996809/154854584-cf3ae60c-7498-4fd2-abab-c5b16c68ffa7.png)

- No of followers for each person :
![2](https://user-images.githubusercontent.com/54996809/154854662-030a3769-38f1-48b2-9ff9-be7d71edc6b7.png)

- No of people each person is following :
![3](https://user-images.githubusercontent.com/54996809/154854721-c32d3e5b-cf81-4360-9543-fe7d4f8265d4.png)

- both followers + following :
![4](https://user-images.githubusercontent.com/54996809/154854775-56a272ca-5841-4c7f-90e5-36f9102a9934.png)

- Min of no of followers + following is 1
- Max of no of followers + following is 1579
- No of persons having followers + following less than 10 are 1320326
- No of weakly connected components 45558

- Number of nodes in the graph with edges 9437519
- Number of nodes in the graph without edges 9437519

- we have a cold start problem here : cold start problem is basically when we don't have any data for some user's or items

## Feature engineering on Graphs :
- Similarity measures :-
    - Jaccard Distance : larger the Jaccard Distance ==> higher the probability that there exist an edge between these two vertices(here,u1 and u2)
    - Cosine distance : 
- Ranking Measures :-
    - Page Ranking :
- Other Graph Features :-
    - Shortest path : Getting Shortest path between two nodes, if nodes have direct path i.e directly connected then we are removing that edge and calculating path.
    - Connected-components (Checking for same community) : for weekly connected component, ignore the direction
    - Adamic/Adar Index : Adamic/Adar measures is defined as inverted sum of degrees of common neighbours for given two vertices.
    - Is person was following back :
    - Katz Centrality :  Katz centrality computes the centrality for a node based on the centrality of its neighbors. It is a generalization of the eigenvector centrality.
    - HITS Score : The HITS algorithm computes two numbers for a node. Authorities estimates the node value based on the incoming links. Hubs estimates the node value based on outgoing links.

- Adding a set of features (compute_features_stage1) :
  - jaccard_followers
  - jaccard_followees
  - cosine_followers
  - cosine_followees
  - num_followers_s
  - num_followees_s
  - num_followers_d
  - num_followees_d
  - inter_followers
  - inter_followees

- Adding new set of features (storage_sample_stage2) :
  - adar index
  - is following back
  -belongs to same weakly connect components
  - shortest path between source and destination

- Adding new set of features (storage_sample_stage3) :
  - Weight Features
    - weight of incoming edges
    - weight of outgoing edges
    - weight of incoming edges + weight of outgoing edges
    - weight of incoming edges * weight of outgoing edges
    - 2*weight of incoming edges + weight of outgoing edges
    - weight of incoming edges + 2*weight of outgoing edges
    - Page Ranking of source
  - Page Ranking of dest
  - katz of source
  - katz of dest
  - hubs of source
  - hubs of dest
  - authorities_s of source
  - authorities_s of dest

## Modelling :
- The most important part of this case studies is featurization, modelling is a straight forward things
- RandomForestClassifier :
  - Train f1 score 0.9652533106548414
  - Test f1 score 0.9241678239279553

![5](https://user-images.githubusercontent.com/54996809/154855898-5d4f7bfd-da9c-49ff-a19b-498ce8b96a5e.png)

- Feature importance : Here, follows_back is the most important feature.
![6](https://user-images.githubusercontent.com/54996809/154855955-45b3ccbb-7fb1-4c13-a629-64f99d15542a.png)







