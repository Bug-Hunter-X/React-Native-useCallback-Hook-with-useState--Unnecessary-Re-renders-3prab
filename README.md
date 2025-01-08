# React Native useCallback Hook with useState: Unnecessary Re-renders

This repository demonstrates a common performance issue in React Native applications when using the `useCallback` hook with functions that internally use the `useState` hook.

## Problem
The `useCallback` hook is designed to memoize functions, preventing unnecessary re-renders. However, if the function's internal state changes on every render, even with `useCallback`, the function will be re-created every time. This happens because `useCallback` only memoizes the function itself, not its closure. The closure in this case includes the state variable.

## Solution
The solution is to add all variables from the closure that change over time to `useCallback`'s dependency array. In the example, `count` is that variable.  Moving the `setCount` state update into a separate function which is then called from within the callback also helps in cases where this is not directly possible. 

## How to Reproduce
1. Clone this repository.
2. Run `npm install`.
3. Run `npx react-native run-android` or `npx react-native run-ios`.
4. Observe the performance issue.  

## Additional Notes
This problem can be subtle and challenging to track down.  Always carefully consider the dependencies passed to `useCallback` to ensure you're correctly memoizing the function.