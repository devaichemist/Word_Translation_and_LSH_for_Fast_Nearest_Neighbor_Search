# Word Translation and LSH for Fast Nearest Neighbor Search

In this Jupyter Notebook, we build a simple machine translation model using word embeddings to translate words between English and French, and then apply Locality-Sensitive Hashing (LSH) to perform fast, approximate nearest neighbor search for translated words. The project demonstrates how vector spaces capture meaning across languages and how efficient search techniques can scale these models.

<img width="752" height="316" alt="Screenshot 2025-11-01 at 23 19 24" src="https://github.com/user-attachments/assets/3943bc91-abe2-48b7-aed0-b1571d35ae72" />

## Steps for building the Naive Machine Translation and LSH model:

1. ### Load the data 
    Import pre-trained English and French word embeddings, along with a bilingual dictionary that maps English words to their French translations.
2. ### Inspect the data 
    Explore the structure and dimensions of the embedding files, check example word pairs, and confirm that both languages have aligned vocabularies.
3. ### Create subsets for training and testing 
    Split the bilingual dictionary into training, development, and test sets to evaluate how well the model generalizes to unseen word pairs.
4. ### Build embedding matrices 
    Construct aligned matrices of English and French word vectors, where each row corresponds to a word pair from the training set.
5. ### Model translation as a linear transformation 
    Represent translation as learning a transformation matrix W that maps English embeddings into the French embedding space by minimizing the difference between predicted and actual French vectors.
6. ### Compute the loss and gradient 
    Implement a loss function based on the Frobenius norm, compute its gradient with respect to W, and optimize it using gradient descent to learn the best transformation.
7. ### Translate words using nearest neighbors 
    Multiply English embeddings by the learned matrix W and find the most similar French vectors using cosine similarity (exact k-nearest neighbors).
8. ### Identify the efficiency problem 
        Exact nearest neighbor search requires comparing each translated vector with every French embedding — a process that becomes very slow for large vocabularies.
To make it faster, we introduce Locality-Sensitive Hashing (LSH), which uses random hyperplanes to split the vector space and group similar embeddings into the same hash buckets for quicker lookup.

<img width="1076" height="508" alt="Screenshot 2025-11-03 at 08 35 02" src="https://github.com/user-attachments/assets/e4cc37e5-7c88-44cd-8eee-381b130262ad" />

9. ### Implement Locality-Sensitive Hashing (LSH) 
    Use random hyperplanes to generate hash values that group similar vectors into the same “buckets,” allowing quick retrieval of potential neighbors.
10. ### Build hash tables and perform approximate search 
    Construct multiple LSH tables to improve reliability, store all French embeddings in them, and perform approximate k-NN search by examining only candidates from matching buckets.
    
    <img width="682" height="218" alt="Screenshot 2025-11-03 at 08 35 32" src="https://github.com/user-attachments/assets/79b7f5de-78b9-4332-821d-8242164c58d7" />

11. ### Evaluate translation accuracy and efficiency 
    Compare the results of exact versus LSH-based approximate nearest neighbor searches, analyzing the trade-off between speed and accuracy in translation retrieval.

## Results
The learned transformation matrix effectively aligns English and French word embeddings, enabling accurate word-to-word translation. Locality-Sensitive Hashing significantly speeds up similarity search with minimal loss in accuracy, demonstrating how mathematical optimization and efficient data structures can work together in natural language processing.


