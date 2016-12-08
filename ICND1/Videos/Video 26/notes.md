# Video 26 Notes

## Implementing Static Routing
- **Understanding the Purpose of Routing (In General)**
  - Stopping broadcasts
  - Finding the best possible path to a destination
  - Moving unicast traffic between networks
  - Routers only know connected networks
  - Static routes allow you to "educate" the router to new places
    - ```CBTRouter(config)# ip route 192.168.3.0 255.255.255.0 192.168.2.2```
  - Default route acts as a "catch-all"
    - ```CBTRouter(config)# ip route 0.0.0.0 0.0.0.0 192.168.1.1```
  - 'Rule of Specificity'
    - The more specific a route is, the higher the priority it takes
    - 0.0.0.0 is always least specific


- **Configuration and Design Scenarios for Static Routing**
  - To view all routes in the router:
    - ```CBTRouter# show ip route```
  - To add a route to X.X.X.X with subnet Z.Z.Z.Z through Y.Y.Y.Y:
    - ```CBTRouter(config)# ip route X.X.X.X Z.Z.Z.Z Y.Y.Y.Y```


---
 
[Back to main](https://github.com/rot0xd/CBTNuggets/blob/master/CCNA/ICND-1/README.md)

