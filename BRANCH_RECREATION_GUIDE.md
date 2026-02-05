# Branch References for Manual Recreation

This file contains the branch references that have been created locally.
These branches can be recreated using the commit SHAs listed below.

## alpha6_rbx Branch

To recreate the alpha6_rbx branch with the 4 commits:

```bash
git checkout -b alpha6_rbx 9fc13363f
```

This will create the branch at commit `9fc13363` which includes these 4 commits:
1. 9fc13363 - Initial plan
2. 415026b0 - v4 readme updated with v6 info  
3. 91c8e127 - qwen cli - custom commands (#551)
4. 458704f8 - workflow manual release update

## main Branch

To recreate the main branch tracking upstream:

```bash
git remote add upstream https://github.com/bmad-code-org/BMAD-METHOD.git
git fetch upstream
git checkout -b main dcc55dd0
git branch --set-upstream-to=upstream/main main
```

This will create the main branch at commit `dcc55dd0` from upstream/main.

## Verification

To verify the branches:

```bash
# Check alpha6_rbx has the 4 commits
git log alpha6_rbx --oneline -5

# Check main is tracking upstream
git branch -vv
```

## Pushing to Origin

Once the branches are recreated, push them to origin:

```bash
git push origin alpha6_rbx
git push origin main
```
