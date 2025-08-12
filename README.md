# data-structure-repo
Algorithms for Programming Problems
This document contains the algorithms for two problems: calculating the sum of distinct elements from two sets and determining if vectors are orthogonal.

Problem 1: Sum of Distinct Elements
The following algorithm calculates the sum of all elements that are present in either of two given sets, but not in both. It works by iterating through each set and checking for the presence of each element in the other set.

ALGORITHM Distinct_Sum_of_Sets
VAR
    set1 : ARRAY OF INTEGER[4] := {3, 1, 7, 9};
    set2 : ARRAY OF INTEGER[5] := {2, 4, 1, 9, 3};
    sum : INTEGER := 0;
    i, j : INTEGER;
    is_common : BOOLEAN;

BEGIN
    // Add elements from set1 that are not in set2
    FOR i FROM 0 TO LENGTH(set1) - 1 DO
        is_common := FALSE;
        FOR j FROM 0 TO LENGTH(set2) - 1 DO
            IF set1[i] == set2[j] THEN
                is_common := TRUE;
                BREAK;
            END_IF
        END_FOR
        IF NOT is_common THEN
            sum := sum + set1[i];
        END_IF
    END_FOR

    // Add elements from set2 that are not in set1
    FOR i FROM 0 TO LENGTH(set2) - 1 DO
        is_common := FALSE;
        FOR j FROM 0 TO LENGTH(set1) - 1 DO
            IF set2[i] == set1[j] THEN
                is_common := TRUE;
                BREAK;
            END_IF
        END_FOR
        IF NOT is_common THEN
            sum := sum + set2[i];
        END_IF
    END_FOR

    Write("The sum of all distinct elements is: ", sum);
END

Problem 2: Dot Product and Orthogonal Vectors
This section includes the procedure and functions for calculating the dot product, along with two main algorithms for checking vector orthogonality.

2.1 Dot Product Procedure
This procedure calculates the dot product of two vectors and stores the result in a variable passed by reference (VAR ps).

PROCEDURE dot_product(v1, v2 : ARRAY OF REAL, VAR ps : REAL, size : INTEGER)
VAR
    i : INTEGER;
BEGIN
    ps := 0;
    FOR i FROM 0 TO size - 1 DO
        ps := ps + v1[i] * v2[i];
    END_FOR
END

2.2 Orthogonality Check with Procedure
This algorithm reads in vector pairs and uses the dot_product procedure to check for orthogonality.

ALGORITHM Orthogonal_Checker_Procedure
VAR
    n : INTEGER;
    v1, v2 : ARRAY OF REAL[100];
    ps : REAL;
    i, j, vector_size : INTEGER;

BEGIN
    Write("Enter the number of vector pairs to check: ");
    Read(n);

    FOR i FROM 1 TO n DO
        Write("Enter the size of vectors for pair ", i, ": ");
        Read(vector_size);

        Write("Enter the elements for vector 1: ");
        FOR j FROM 0 TO vector_size - 1 DO
            Read(v1[j]);
        END_FOR

        Write("Enter the elements for vector 2: ");
        FOR j FROM 0 TO vector_size - 1 DO
            Read(v2[j]);
        END_FOR

        dot_product(v1, v2, ps, vector_size);

        IF ps == 0 THEN
            Write("Pair ", i, ": The vectors are orthogonal.");
        ELSE
            Write("Pair ", i, ": The vectors are not orthogonal.");
        END_IF
    END_FOR
END

2.3 Orthogonality Check with Function
This modified version uses a function to calculate and return the dot product, which is then used in the main algorithm.

FUNCTION dot_product_function(v1, v2 : ARRAY OF REAL, size : INTEGER) : REAL
VAR
    sum : REAL := 0;
    i : INTEGER;
BEGIN
    FOR i FROM 0 TO size - 1 DO
        sum := sum + v1[i] * v2[i];
    END_FOR
    RETURN sum;
END

ALGORITHM Orthogonal_Checker_Function
VAR
    n : INTEGER;
    v1, v2 : ARRAY OF REAL[100];
    result : REAL;
    i, j, vector_size : INTEGER;

BEGIN
    Write("Enter the number of vector pairs to check: ");
    Read(n);

    FOR i FROM 1 TO n DO
        Write("Enter the size of vectors for pair ", i, ": ");
        Read(vector_size);

        Write("Enter the elements for vector 1: ");
        FOR j FROM 0 TO vector_size - 1 DO
            Read(v1[j]);
        END_FOR

        Write("Enter the elements for vector 2: ");
        FOR j FROM 0 TO vector_size - 1 DO
            Read(v2[j]);
        END_FOR

        result := dot_product_function(v1, v2, vector_size);

        IF result == 0 THEN
            Write("Pair ", i, ": The vectors are orthogonal.");
        ELSE
            Write("Pair ", i, ": The vectors are not orthogonal.");
        END_IF
    END_FOR
END
