# 🧩 The Random Image Puzzle Challenge

[Google Collab Link](https://colab.research.google.com/github/UCU-CSEA/UCU-Code-Challenge-Season-1/blob/main/puzzle.ipynb))

## Introduction

The overall goal is to reconstruct the original image by correcting the sequence and orientation of the fragmented pieces.

Puzzle Parameters

The original image is subjected to the following fragmentation:

Original Image Size: $450 \times 450$ pixels.

Number of Pieces ($n$): $81$ pieces (creating a perfect $9 \times 9$ grid).

Individual Piece Size: Each piece is an array of approximately $50 \times 50 \times 3$ (Height x Width x RGB) in size.

Creation Process and Data Structure

The Canvas script executes a three-step scrambling process:

1. Breakdown and Assign (The Order Problem)

The image is segmented into 81 pieces. Each piece is associated with a Correct Order Index ($\mathbf{k}$), a unique integer from 1 to 81, representing its original position in the $9 \times 9$ grid (reading left-to-right, top-to-bottom).

2. Transform (The Rotation Problem)

A random rotation from the set $\mathbf{S}_{rot} = \{0^\circ, 90^\circ, 180^\circ, 270^\circ\}$ is applied to the image data (the NumPy matrix) of every piece. The angle applied is stored as Applied Rotation ($\theta$).

3. Shuffle (The Scrambled Array)

The collection of 81 pieces is randomly re-ordered using the Fisher-Yates shuffle, resulting in the final scrambled array, $\mathbf{A}_{puzzle}$.

Each element in $\mathbf{A}_{puzzle}$ is a tuple containing:

$$\text{Piece}_i = (\text{Rotated RGB Matrix}, \mathbf{k}, \theta)$$

🎯 Challenge Goals for the Solver

A complete solution requires two distinct algorithmic steps to reverse the scrambling:

Challenge 1: Sorting the Array Sequence

The solver must implement a sorting algorithm to re-order the pieces in $\mathbf{A}_{puzzle}$ according to their Correct Order Index ($\mathbf{k}$).

$$\mathbf{A}_{puzzle} \xrightarrow{\text{Sort by } \mathbf{k}} \mathbf{A}_{sorted}$$

Challenge 2: Correcting the Rotation

After the pieces are in the correct sequence, the solver must iterate through $\mathbf{A}_{sorted}$ and apply the inverse rotation to the internal Rotated RGB Matrix to restore its original $0^\circ$ orientation. For example, if $\theta = 270^\circ$ was applied, the solver must apply $90^\circ$ to correct it.

$$\mathbf{A}_{sorted} \xrightarrow{\text{Undo } \theta} \text{Final Reconstructed Image}$$

The file 'scrambled_puzzle_data.pkl contains a log of the dimensions and rotations applied to the first three scrambled pieces, which can be used to verify the data structure and rotation logic.

## Read the Scramble Data Guide in order to use the .pkl file. 
