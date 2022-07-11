- [Branch rule](#branch-rule)
  - [Branch flow](#branch-flow)
  - [Branch merge rule](#branch-merge-rule)
  - [Branching Naming Convention](#branching-naming-convention)
- [Development flow](#development-flow)
  - [Development new feature](#development-new-feature)
  - [Fix bug when the game is running on live](#fix-bug-when-the-game-is-running-on-live)
  - [Resolve code conflicts:](#resolve-code-conflicts)
    - [Resolve conflict when merging from `feature` to `develop`:](#resolve-conflict-when-merging-from-feature-to-develop)
    - [Resolve conflicts when merging from `feature` to `debug`:](#resolve-conflicts-when-merging-from-feature-to-debug)

# Branch rule

## Branch flow

![branch_rule](./snapshot/branch_rule.png)

* `master`: Branch is for release, never push code to this branch. It should be stable all the time and won’t allow any direct check-in. You can only merge it after code review.
* `develop`: Middle branch used to implement the feature, created from branch `master`, all feature branches will merge into this. The `develop` branch’s idea is to make changes in it and restrict the developers from making any changes in the `master` branch directly, then this `develop` branch will merge into `master` branch
* `feature`: Use for feature implement. Created from `develop` branch
* `debug`: Use for external debug, or test play

## Branch merge rule

* When starting project: Create branch `develop` from branch `mater`
```mermaid
graph LR;
    master-->develop;    
```
* When implement feature: Create branch `feature` from branch `develop`
```mermaid
graph LR;
    develop-->feature;    
```
* When release: Merge `feature` into `develop`, then merge `develop` into `master`
```mermaid
graph LR;
    feature-->develop;   
    develop-->master;    
```
* When debug: Merge `feature` into `debug`.
```mermaid
graph LR;
    feature-->debug;    
```

* **Note: When releasing game or play test, need to create branch/tag to store**

## Branching Naming Convention

* All branch names must be in `lowercase`
* Names are separated by `_` and `/`. Eg:
```
fixbug/20220711_button_cant_click
ranking/ranking_implement
inventory/hero_inventory
```
* For release & test play branches, date information in `YYYYMMDD` format is required. Eg:
```
release/20220711_version1
release/20220711_fixbug
test_play/20220711_week1
```

# Development flow

## Development new feature

```mermaid
graph TD;
    id1["Create branch `develop`->`feature`"]
    id2["Implement feature"]
    id3["Merge into `debug` for debugging"]
    id4["Merge into `develop` for review if needed"]
    id5["Merge into `master` for release"]
    id6["Create branch/tag to store"]
    id1 --> id2;      
    id2 --> id3;    
    id3 --> id4;    
    id4 --> id5;    
    id5 --> id6;    
```

## Fix bug when the game is running on live
```mermaid
graph TD;
    id1["Create branch `develop`->`fixbug`"]
    id2["Fix bug in branch"]
    id3["Merge into `debug` for debugging"]
    id4["Merge into `develop` for review if needed"]
    id5["Merge into `master` for release"]
    id6["Create branch/tag to store"]
    id1 --> id2;      
    id2 --> id3;    
    id3 --> id4;    
    id4 --> id5;    
    id5 --> id6;    
```

## Resolve code conflicts:

### Resolve conflict when merging from `feature` to `develop`: 

* Merge branch from branch `develop` into branch `feature`. 
* Manual resolve conflicts on branch `feature`.
* Then merge `feature` back into `develop`

```mermaid
graph TD;
    id1["Merge branch from branch `develop` into branch `feature`"]
    id2["Manual resolve conflicts on branch `feature`"]
    id3["Merge `feature` back into `develop`"]
    id1 --> id2;      
    id2 --> id3;      
```

### Resolve conflicts when merging from `feature` to `debug`: 

* Merge branch from branch `feature` into branch `debug`. 
* Manual resolve conflict on `debug` branch.
* **Never merge branch `debug` into branch `feature` or `develop`. Because the `debug` branch usually contains debug information that doesn't need to be released.**

```mermaid
graph TD;
    id1["Merge branch from branch `feature` into branch `debug`"]
    id2["Manual resolve conflict on `debug` branch"]
    id1 --> id2;         
```
