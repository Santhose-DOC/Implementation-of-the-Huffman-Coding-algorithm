# Experiment 11 -- Implementation of the Huffman Coding Algorithm

### Name: Santhose Arockiaraj J
### RegNo: 212224230248

## Aim

To implement the Huffman Coding algorithm in Python by calculating
character frequencies, constructing a Huffman tree, and generating a
unique binary code for each character.

## Procedure

1.  Initialize the input string as `"huffman coding"`.
2.  Calculate the frequency of each character in the input string using
    a dictionary.
3.  Create tree nodes containing each character and its corresponding
    frequency.
4.  Sort the nodes in ascending order based on their frequencies.
5.  Select the two nodes with the smallest frequencies.
6.  Combine the selected nodes into a new internal node. Set its
    frequency to the sum of the two selected frequencies.
7.  Repeat the sorting and combining process until only one node
    remains. This node represents the Huffman tree.
8.  Generate Huffman codes recursively:
    -   Assign `0` when traversing to the left child.
    -   Assign `1` when traversing to the right child.
    -   Store the generated code when a leaf node (character) is
        reached.
9.  Display each character and its corresponding Huffman code.

## Program

``` python
# Step 1: Get the input string
input_string = "Santhose Arockiaraj J"  # Example input string

# Step 2: Calculate frequency of each character in the input string
frequency = {}
for char in input_string:
    if char in frequency:
        frequency[char] += 1
    else:
        frequency[char] = 1

# Step 3: Create tree nodes
nodes = [[char, freq] for char, freq in frequency.items()]

# Step 4: Main function to implement Huffman coding
while len(nodes) > 1:
    # Sort nodes based on frequency
    nodes = sorted(nodes, key=lambda x: x[1])

    # Pick two smallest nodes
    left = nodes.pop(0)
    right = nodes.pop(0)

    # Create a new node with combined frequency
    new_node = [[left, right], left[1] + right[1]]
    nodes.append(new_node)

# The final node is the Huffman tree
huffman_tree = nodes[0]

# Step 5: Generate Huffman codes
huffman_codes = {}

def generate_codes(tree, code=""):
    if isinstance(tree[0], str):  # If it's a leaf node
        huffman_codes[tree[0]] = code
    else:  # If it's an internal node, recurse
        generate_codes(tree[0][0], code + "0")
        generate_codes(tree[0][1], code + "1")

generate_codes(huffman_tree)

# Step 6: Print the characters and their Huffman codes
print("Character | Huffman Code")
print("-------------------------")
for char, code in huffman_codes.items():
    print(f"    {char}    |    {code}")
```

## Output

The program displays a table containing each distinct character in the
input string and its corresponding Huffman binary code.

<img width="192" height="327" alt="image" src="https://github.com/user-attachments/assets/6471ece0-c485-4418-83c3-15bbec10ff75" />



The generated binary codes depend on the order in which nodes with equal
frequencies are combined. The program prints the actual codes produced
during execution.

## Result

Thus, the Huffman Coding algorithm was implemented successfully in
Python. Character frequencies were calculated, a Huffman tree was
constructed by repeatedly combining the two least-frequent nodes, and
binary Huffman codes were generated and displayed for each character.
