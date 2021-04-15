# Episode ### : Title
- https://www.youtube.com/watch?v=30EQwXvo9KM
- Hosted by Taylor
- 15/04/2021

## Show Notes

7.2.0 - https://github.com/concourse/concourse/releases/tag/v7.2.0
- all steps wait for a worker! No more failing steps when there are no workers. Also means steps could wait for a very long time...
- LDAP as password connector for fly. Either local user (default) or ldap. Configure on web


Container Placement Strategies (6 in total):
- volume-locality (default)
    pros: fast initialziation time for steps (task and put)
    cons: workers are more likely to fall over
    - order-only
- random
    pros: even load distribution across workers
    cons: longer initialziation time for steps because volumes constantly need to be streamed

remainder are all focused on not putting work on a worker that may be close to being overloaded
- fewest-build-containers
    - order-only
- limit-active-tasks
    - affects all steps, NOT just task steps.
    - task steps will be blocked if all workers are at max tasks 
    - check, put, get steps will not be blocked, they will be scheduled on the worker with the fewest tasks
    - filter AND order
- limit-active-containers
    - filter-only
- limit-active-volumes
    - filter-only

Talk about chaining vs not chaining

All strategies order everything in the chain and then we ask all strategies if they approve of the worker based on their ordering
