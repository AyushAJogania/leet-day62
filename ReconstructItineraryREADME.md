# leet-day62

# Reconstruct Itinerary - LeetCode

## Problem Description

You are given a list of airline tickets where `tickets[i] = [fromi, toi]` represent the departure and arrival airports of one flight. Reconstruct the itinerary in order and return it.

All of the tickets belong to a man who departs from "JFK", thus, the itinerary must begin with "JFK". If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string.

### Example

#### Input

```cpp
tickets = [["MUC","LHR"],["JFK","MUC"],["SFO","SJC"],["LHR","SFO"]]
```

#### Output

```cpp
["JFK","MUC","LHR","SFO","SJC"]
```

### Constraints

- 1 <= tickets.length <= 300
- tickets[i].length == 2
- fromi.length == 3
- toi.length == 3
- fromi and toi consist of uppercase English letters.
- fromi != toi

## Solution Approach

The problem can be solved by constructing a graph of airports and using a depth-first search (DFS) approach to find the itinerary. Here's how the solution works:

1. Build a graph where each airport is a node, and directed edges represent flight connections. Use a multiset to store destinations for each airport, ensuring the smallest lexical order.

2. Start the DFS traversal from the "JFK" airport. While there are destinations from the current airport, remove the destination with the smallest lexical order and continue the traversal.

3. Keep adding airports to the itinerary as you traverse. Since the DFS goes as far as possible before backtracking, the itinerary will be built in reverse order.

4. Reverse the itinerary to get the correct order, starting from "JFK."

## Pseudocode

1. Create an empty graph as an unordered map where keys are airport names, and values are multisets to store destinations.

2. Populate the graph by iterating through the tickets and adding destinations to the corresponding airport's multiset.

3. Start the DFS traversal from "JFK":
   - While there are destinations from the current airport:
     - Remove the smallest lexical destination from the multiset.
     - Recursively call the DFS on the removed destination.

4. Reverse the itinerary to get the correct order.

5. Return the itinerary as a vector of strings.

## Time Complexity

The time complexity of this solution is O(N log N), where N is the number of tickets. The DFS visits each ticket once, and finding the smallest lexical order destination takes O(log N) time.

