Git has a way to limit checkout to files that match certain patterns called [sparse checkout](https://git-scm.com/docs/git-read-tree#_sparse_checkout).

## Instructions

1. Follow the standard instructions here: [Campus Web Hosting Repo Creator](https://bitbucket.org/muwebcom/vh-repo-creator/overview/).
2. Run the following command: `git config core.sparseCheckout true`
3. Create the following file: `.git/info/sparse-checkout`

The `sparse-checkout` file should contain a list of patterns you want your files to match. These can be both positive and negative patterns, but you **must** have at least one positive pattern for it to work.

If you **only** want the `marcom.missouri.edu` folder to publish, this pattern will work:

```
marcom.missouri.edu/*
```

Alternatively, you could specifically exclude certain folders and files:

```
/*
!gulpfile.js
!README.md
!src/*
```