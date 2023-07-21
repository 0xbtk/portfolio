| Total Stylistic issues |
|------------------------|

| Risk    | Issues Details                                                                                          | Number        |
|---------|---------------------------------------------------------------------------------------------------------|---------------|
| [S-**]  | Lines are too long                                                                                      |               |
| [S-**]  | Function writing does not comply with the `Solidity Style Guide`                                        |               |
| [S-**]  | Add `I` prefix to interface contracts                                                                   |               |
| [S-**]  | Generate perfect code headers every time                                                                |               |
| [S-**]  | For functions, follow Solidity standard naming conventions                                              |               |

## [S-**] Lines are too long

#### Description

Usually lines in source code are limited to 80 characters. Today's screens are much larger so it's reasonable to stretch this in some cases. Since the files will most likely reside in GitHub, and GitHub starts using a scroll bar in all cases when the length is over 164 characters, the lines below should be split when they reach that length.

> Ref: https://docs.soliditylang.org/en/v0.8.10/style-guide.html#maximum-line-length

#### Lines of code 

- []()

## [S-**] Function writing does not comply with the `Solidity Style Guide`

#### Description

Ordering helps readers identify which functions they can call and to find the constructor and fallback definitions easier. But there are contracts in the project that do not comply with this.

Functions should be grouped according to their visibility and ordered:

- `constructor()`
- `receive()`  
- `fallback()`  
- `external / public / internal / private`
- `view / pure`

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Follow Solidity Style Guide.

## [S-**] Add `I` prefix to interface contracts

#### Description

Filename prefixed by `I` usually indicates an interface rather than a contract.

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Add `I` prefix to interface contracts.

## [S-**] Generate perfect code headers every time

#### Description

I recommend using header for Solidity code layout and readability

> Ref: https://github.com/transmissions11/headers

#### Lines of code 

- []()

#### Recommended Mitigation Steps

```
/*//////////////////////////////////////////////////////////////
                           TESTING 123
//////////////////////////////////////////////////////////////*/
```

## [S-**] For functions, follow Solidity standard naming conventions

#### Description

The protocol don't follow solidity standard naming convention.

> Ref: https://docs.soliditylang.org/en/v0.8.17/style-guide.html#naming-conventions

#### Lines of code 

- []()

#### Recommended Mitigation Steps

Follow solidity standard [naming convention](https://docs.soliditylang.org/en/v0.8.17/style-guide.html#naming-conventions).
