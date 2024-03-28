
# Federated Learning Framework

## Introduction
This project is a federated learning framework that allows for distributed machine learning across multiple machines. It enables training models on decentralized data while maintaining privacy and security. For a more detailed explanation of this project, please refer to the [final report](final_paper.pdf).

## General Architecture
This architecture consists of a coordinator and multiple workers. The coordinator is responsible for managing the global model and coordinating the training process. Workers are responsible for training the model on their local data and sending updates to the coordinator. With this process,
data is decentralized and never leaves the worker's machine. The coordinator aggregates the updates from the workers and sends the updated model back to the workers. This process is repeated for multiple rounds until the model converges. The coordinator also synchronizes workers to ensure training proceeds in organized rounds. Our implementation uses federated averaging as the aggregator function, which has been shown to perform well for both homogeneous and heterogeneous data settings.

## Implementation
Our architecture was built using Python, XML-RPC, and PyTorch, chosen for their compatibility with popular machine learning frameworks. The implementation is inspired by MapReduce, aiming for modularity and customizability. Machine learning code is distinct from communication and coordination code, allowing for easy specification of different data sources and model configurations. Our system abstracts away the details of coordinating across workers, making it language and framework agnostic.


## Evaluation
For testing, we used the MNIST digits dataset to simplify the machine learning code and focus on the framework for training. Our system is designed to work with nearly any model or dataset. We also added logic so that each machine worked with a random subset of the MNIST dataset, with varied total images for each worker. To facilitate testing on a large number of AWS EC2 machines, we developed several scripts to deploy and run code across all machines.

To test our load balancing system, we recorded the round trip training time for each worker at each epoch. The round trip training time is defined as the total time between when the coordinator sends a set of weights to a worker and when the coordinator receives that worker’s updated weights back. Our load balancing system effectively detected stragglers and reduced their workload, but it may not be granular enough, and this could be improved in the future.

Due to the distributed nature of the system, we needed to be able to tolerate some level of worker failure. We included several fault tolerance mechanisms, such as a built-in retry mechanism for transient network errors or worker-side glitches. For irrecoverable worker failures, the primary fault tolerance mechanism for our system is the quorum protocol. The results show that the quorum protocol gives our system good resilience to irrecoverable worker failures until the percentage of failed workers becomes so great that we are no longer able to achieve a quorum.


## Usage

To deploy: 
- from scripts folder on laptop, `./deploy.sh`

To start: 
- `ssh -i [your private key] [username]@[coordinator IP] <- use this window to monitor coordinator output
- from scripts folder on laptop, `./start.sh`

To shutdown: 
- from scripts folder on laptop, `./shutdown.sh`
