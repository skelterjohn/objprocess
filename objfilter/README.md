
```
$ objfilter --in=rjson --out=rjson 'x.y.z=3' <<< '
{
 x: {
  y: {
   z: 3,
  },
 },
}'
{
 x: {
  y: {
   z: 3,
  },
 },
}
```

```
$ objfilter --in=rjson --out=rjson 'x.y.z=2' <<< '
{
 x: {
  y: {
   z: 3,
  },
 },
}'
```

[] filters a list to those that match
```
$ objfilter --in=rjson --out=rjson 'x[].z=2' <<< '
{
 x: [
  {
   z:1,
  },
  {
   z:2,
  },
 ],
}'
{
 x: [
  {
   z:2,
  },
 ],
}
```

```
$ objfilter --in=rjson --out=rjson 'x[].z=2' <<< '
{
 x: [
  {
   z:2,
  },
 ],
 y: 5,
}'
{
 x: [
  {
   z:2,
  },
 ],
 y: 5,
}
```

```
$ objfilter --in=rjson --out=rjson '[].z=2' <<< '
[
 {
  z: 2,
  x: "hello",
 },
 {
  z: 1,
  x: "hello",
 },
]'
[
 {
  z: 2,
  x: "hello",
 },
]
```

```
$ objfilter --in=rjson --out=rjson '[].z=2' '[].x=1' <<< '
[
 {
  z: 1,
  x: 1,
 },
 {
  z: 2,
  x: 1,
 },
 {
  z: 1,
  x: 2,
 },
 {
  z: 2,
  x: 2,
 },
]'
[
 {
  z: 2,
  x: 1,
 },
]
```

E prints out all indices if one matches the filter.
```
$ objfilter --in=rjson --out=rjson '[E].z=2' '[].x=1' <<< '
[
 {
  z: 1,
  x: 1,
 },
 {
  z: 2,
  x: 1,
 },
 {
  z: 1,
  x: 2,
 },
 {
  z: 2,
  x: 2,
 },
]'
[
 {
  z: 2,
  x: 1,
 },
 {
  z: 1,
  x: 1,
 },
]
```

```
() and (E) are like [] and [E], except for fields instead of indices
$ objfilter --in=rjson '.().(E).z=1' <<< '
{
 x: {
  y: {
   z: 1,
  },
  w: {
   z: 2,
  },
 },
 q: {
  y: {
   z: 2,
  },
 },
}
'
{
 x: {
  y: {
   z: 1,
  },
  w: {
   z: 2,
  },
 },
}
```
