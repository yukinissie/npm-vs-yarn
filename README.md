# npm-vs-yarn

[Npm][1] vs [Yarn][2] install speed testing.

## What is Yarn

Yarn is a new package manager for JavaScript. Please read [blog post][3] from [Facebook][4] for detail information.

[1]: https://www.npmjs.com/
[2]: https://yarnpkg.com/
[3]: https://code.facebook.com/posts/1840075619545360
[4]: https://code.facebook.com/

## Prepare Environment

You can testing in Docker or what you prefer.

- node version: `v20.10.0`
- npm verison: `10.2.3`
- yarn verison: `1.22.21`

## Testing without cache

Testing install speed without cache `node_modules` folder.

```
rm -rf ~/.npm/_cacache/
rm -rf node_modules
time npm install
```

time: `4.88s`

Try [npm ci](https://docs.npmjs.com/cli/ci) command

```
rm -rf ~/.npm/_cacache/
rm -rf node_modules
time npm ci
```

time: `5.02s`

```
yarn cache clean
rm -rf node_modules
time yarn install
```

time: `4.64s`

## Testing with cache

Testing install speed **without** include cache `node_modules` folder.

```
rm -rf node_modules
time npm install
```

time: `2.20s`

Try [npm ci](https://docs.npmjs.com/cli/ci) command

```
rm -rf node_modules
time npm ci
```

time: `2.18s`

```
rm -rf node_modules
time yarn install
```

time: `1.68s`

Testing install speed **with** cache `node_modules` folder.

```
time npm install
```

time: `0.79s`

```
time npm ci
```

time: `2.46s`

```
time yarn install
```

time: `0.10s`

## Conclusion

Date: 2023-11-26

Yarn is faster than npm. We can move package manager from Npm to Yarn for JavaScript now.

|                                              | npm install | npm ci | yarn  |
| -------------------------------------------- | ----------- | ------ | ----- |
| install without cache (without node_modules) | 4.88s       | 5.02s  | 4.64s |
| install with cache (without node_modules)    | 2.20s       | 2.18s  | 1.68s |
| install with cache (with node_modules)       | 0.79s       | 2.46s  | 0.43s |
| install without internet (with node_modules) | 0.85s       | 2.40s  | 0.10s |
