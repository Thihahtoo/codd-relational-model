# Codd's Relational Model

## Background

Codd's relational model forms the basis of SQL databases and is one of the most commonly used data models.

In this model, a database is composed of relations. A relation can be thought of as a table, but to be more precise, it has a schema, which is a set of attributes, and an instance, which is a set of tuples corresponding to the attributes.  
For example, let <b><i>R</i></b> be

|<i>A</i>|<i>B</i>|
|---|---|
|1|2|
|3|4|

and let <b><i>S</i></b> be

|<i>B</i>|<i>C</i>|
|---|---|
|2|1|
|6|8|

The schema of <b><i>R</i></b> is <b>\{ A, B \}</b>, and the instance of <b><i>R</i></b> is <b>\{ (1,2), (3,4) \}</b>. The schema of <b><i>S</i></b> is <b>\{ B, C \}</b>, and the instance of <b><i>S</i></b> is <b>\{ (2,1), (6,8) \}</b>. Although the schema is a set, its order should be consistent with the tuples in the instance. If we change the order in the schema, we also have to change the order of the tuples in the instance. The following is another representation of <b><i>R</i></b>.

|<i>B</i>|<i>A</i>|
|---|---|
|2|1|
|4|3|

Since the set of tuples is a set, the order of the "rows" is not important, and there are no "duplicate rows".

## Operations

The relational algebra has the following operations:

1. Selection ($\sigma$)
2. Projection ($\pi$)
3. Rename ($\rho$)
4. Cartesian product ($\times$)
5. Union ($\cup$)
6. Difference ($-$)

The first three are unary operations (requiring one operand), and the others are binary operations (requiring two operands). Each operand is a relation, and the result of each operation is also a relation.

### 1. Selection (\sigma)

Selection picks tuples satisfying a condition. For example, $\sigma_{A>1}R$ results in

$$
\begin{array}{c|c}
A&B\\
\hline
3&4\\
\end{array}
$$

### 2. Projection ($\pi$)

Projection picks attributes. For example, $\pi_AR$ results in

$$
\begin{array}{c|c}
A\\
\hline
1\\
3
\end{array}
$$

### 3. Rename ($\rho$)

Rename changes the names of the attributes in the schema. For example, $\rho_{C\to A}S$ results in

$$
\begin{array}{c|c}
B&A\\
\hline
2&1\\
6&8
\end{array}
$$

### 4. Union ($\cup$)

Union gives tuples that are in any of its operands, but it requires that the schemata of the operands match. For example, $R\cup S$ is not allowed because the schema of $R$ ($\{A,B\}$) is different from that of $S$ ($\{B,C\}$). However, we can apply rename to $S$ and then apply union: $R\cup(\rho_{C\to A}S)$ results in

$$
\begin{array}{c|c}
A&B\\
\hline
1&2\\
3&4\\
8&6
\end{array}
$$

### 5. Difference ($-$)

Difference gives tuples that are in the first operand but not in the second operand. As with union, it requires that the schemata of the operands match. For example, $R-S$ is not allowed because the schema of $R$ ($\{A,B\}$) is different from that of $S$ ($\{B,C\}$). However, we can apply rename to $S$ and then apply difference: $R-(\rho_{C\to A}S)$ results in

$$
\begin{array}{c|c}
A&B\\
\hline
3&4\\
\end{array}
$$

### 6. Cartesian product ($\times$)

Cartesian product gives tuples resulting from concatenation of two tuples, one from each operand. If there are common attributes, the attribute is prefixed with the name of the relation it comes from followed by a dot. For example, $R\times S$ results in


$$
\begin{array}{c|c}
A&R.B&S.B&C\\
\hline
1&2&2&4\\
1&2&6&8\\
3&4&2&4\\
3&4&6&8
\end{array}
$$
