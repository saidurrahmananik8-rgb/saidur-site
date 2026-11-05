# How to change this site safely

`main` is **live**. Every push to `main` goes straight to https://saidursite.vercel.app.
`main` is protected: direct pushes are rejected, so changes go through `dev` and a pull request.

## The loop

```bash
cd ~/Downloads/pabna-site

git checkout main          # always start from the live version
git pull                   # make sure it is current
git checkout dev           # switch to the working branch
git merge main             # bring dev up to date (skip if it already is)

# ... edit index.html / assets ...

git add -A
git commit -m "What you changed, in plain words"
git push                   # dev -> Vercel builds a PREVIEW url
```

Open Vercel -> Deployments -> the newest row marked **Preview**. Check it on your phone.
The live site has not changed.

## Publish (when the preview looks right)

1. GitHub -> **Pull requests** -> **New pull request**
2. base: **main**  ←  compare: **dev**
3. Read the diff (red = removed, green = added)
4. **Create pull request** -> **Merge pull request**

Vercel deploys `main` about 20 seconds later. `dev` is deleted automatically after the merge.

## Emergency

- Wrong version live? Vercel -> Deployments -> the older good one -> menu -> **Promote to Production**
- Need to bypass the protection? GitHub -> Settings -> Branches -> edit/disable the `main` rule.
  Turn it back on afterwards.

## What not to do

- Do not `git push` while on `main` — it will be rejected (that is the point).
- Do not commit `.xlsx` / `.csv` files. `.gitignore` already blocks them: client lead lists must never be public.
- Do not edit files directly in the GitHub web editor on `main` — use `dev`.
