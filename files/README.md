I have a string that looks as follows:

```ts
const str = `2019,Level 1,99999,All industries,Dollars (millions),H01,Total income,Financial performance,"728,239","ANZSIC06 divisions A-S (excluding classes K6330, L6711, O7552, O760, O771, O772, S9540, S9601, S9602, and S9603)"
`;
```

I want to split this string based on a delimiter `,` using the `split(delimeter)` method but also ignore the `","` that is in `quotes ("")`. I want the result to be an array of strings that looks as follows:

```ts
[
  "2019",
  "Level 1",
  "99999",
  "All industries",
  "Dollars (millions)",
  "H01",
  "Total income",
  "Financial performance",
  "728,239",
  "ANZSIC06 divisions A-S (excluding classes K6330, L6711, O7552, O760, O771, O772, S9540, S9601, S9602, and S9603)",
];
```
