# ExpNo:10 Implementation of Classical Planning Algorithm
# Algorithm or Steps Involved:
<ol>
  <li>Define the initial state</li>
  <li>Define the goal state</li>
  <li>Define the actions</li>
  <li>Find a <b>plan</b> to reach the goal state</li>
  <li>Print the plan</li>
</ol>

# Example - 1
```
initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'B', 'B': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B']
```
# Example - 2
```
initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B', 'move_B_to_C']
```

<h3>Program</h3>

```py
from collections import deque

def find_plan(initial_state, goal_state, actions):

    # Check whether the goal is reached
    def is_goal(state):
        for key, value in goal_state.items():
            if state.get(key) != value:
                return False
        return True

    # Apply an action to a state
    def apply_action(state, action):
        new_state = state.copy()

        for key, value in action['effect'].items():
            new_state[key] = value

        return new_state

    # Check whether action preconditions are satisfied
    def is_applicable(state, action):
        for key, value in action['precondition'].items():
            if state.get(key) != value:
                return False
        return True

    # Queue contains (state, plan)
    queue = deque()
    queue.append((initial_state, []))

    # Store visited states
    visited = set()

    while queue:

        state, plan = queue.popleft()

        # Convert state to a hashable form
        state_key = tuple(sorted(state.items()))

        if state_key in visited:
            continue

        visited.add(state_key)

        # Goal reached
        if is_goal(state):
            return plan

        # Try every action
        for action_name, action in actions.items():

            if is_applicable(state, action):

                new_state = apply_action(state, action)
                new_plan = plan + [action_name]

                queue.append((new_state, new_plan))

    return None


# Example 1
initial_state = {
    'A': 'Table',
    'B': 'Table'
}

goal_state = {
    'A': 'B',
    'B': 'Table'
}

actions = {
    'move_A_to_B': {
        'precondition': {
            'A': 'Table',
            'B': 'Table'
        },
        'effect': {
            'A': 'B'
        }
    },

    'move_B_to_Table': {
        'precondition': {
            'A': 'Table',
            'B': 'B'
        },
        'effect': {
            'B': 'Table'
        }
    }
}

plan = find_plan(initial_state, goal_state, actions)

print("Plan:", plan)
```

```py
from collections import deque

def find_plan(initial_state, goal_state, actions):

    # Check whether the goal is reached
    def is_goal(state):
        for key, value in goal_state.items():
            if state.get(key) != value:
                return False
        return True

    # Apply an action to a state
    def apply_action(state, action):
        new_state = state.copy()

        for key, value in action['effect'].items():
            new_state[key] = value

        return new_state

    # Check whether action preconditions are satisfied
    def is_applicable(state, action):
        for key, value in action['precondition'].items():
            if state.get(key) != value:
                return False
        return True

    # Queue contains (state, plan)
    queue = deque()
    queue.append((initial_state, []))

    # Store visited states
    visited = set()

    while queue:

        state, plan = queue.popleft()

        # Convert state to a hashable form
        state_key = tuple(sorted(state.items()))

        if state_key in visited:
            continue

        visited.add(state_key)

        # Goal reached
        if is_goal(state):
            return plan

        # Try every action
        for action_name, action in actions.items():

            if is_applicable(state, action):

                new_state = apply_action(state, action)
                new_plan = plan + [action_name]

                queue.append((new_state, new_plan))

    return None


initial_state = {
    'A': 'Table',
    'B': 'Table',
    'C': 'Table'
}

goal_state = {
    'A': 'B',
    'B': 'C',
    'C': 'Table'
}

actions = {
    'move_A_to_B': {
        'precondition': {
            'A': 'Table',
            'B': 'Table'
        },
        'effect': {
            'A': 'B'
        }
    },

    'move_B_to_C': {
        'precondition': {
            'A': 'B',
            'B': 'Table',
            'C': 'Table'
        },
        'effect': {
            'B': 'C'
        }
    },

    'move_C_to_Table': {
        'precondition': {
            'A': 'B',
            'B': 'C',
            'C': 'C'
        },
        'effect': {
            'C': 'Table'
        }
    }
}

plan = find_plan(initial_state, goal_state, actions)

print("Plan:", plan)

plan = find_plan(initial_state, goal_state, actions)

print("Plan:", plan)
```

<h3>output</h3>
<img width="463" height="237" alt="image" src="https://github.com/user-attachments/assets/c00046c6-7e92-45de-ba95-f06ae3df3354" />

<img width="575" height="270" alt="image" src="https://github.com/user-attachments/assets/e2394dd4-a7b5-4154-a0b8-d015c9d112bd" />

<h3>Result</h3>

Thus, the Classical Planning Algorithm was successfully implemented using Python, and a sequence of actions was generated to transform the initial state into the goal state.
