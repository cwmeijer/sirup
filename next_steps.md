# Next steps

## Put the generated files under version control

Once your Python package is created, put it under [version
control](https://guide.esciencecenter.nl/#/best_practices/version_control) using
[git](https://git-scm.com/) and [GitHub](https://github.com/).

Note that the next step assumes you have setup your connection to GitHub via SSH,
see [Connecting to GitHub with SSH](https://docs.github.com/en/github-ae@latest/authentication/connecting-to-github-with-ssh).

Alternatively, you can also use a personal access token, see
[Creating a personal access token](https://docs.github.com/en/github-ae@latest/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).  If you choose this option, below you will have to replace
`git@github.com:` by `https://github.com/`.

```shell
cd sirup
git init
git add --all
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:ivory-tower-private-power/sirup
```

## Push the initial commit to a new repo on GitHub

Go to
[https://github.com/organizations/ivory-tower-private-power/repositories/new](https://github.com/organizations/ivory-tower-private-power/repositories/new)
and create a new repository named `sirup` as an empty repository, then push your commits to GitHub:

```shell
git push --set-upstream origin main
```

## Check automatically generated issues

A short while after you push your commits to GitHub for the first time, a few issues outlining next steps will added
automatically ([here](https://github.com/ivory-tower-private-power/sirup/issues?q=author%3Aapp%2Fgithub-actions)). Resolve them to complete the
setup of your repository.

## Project development documentation

The [README.dev.md](README.dev.md) contains developer documentation.

## Project layout explained

For an explanation of what files are there, and what each of these do, please refer to [project_setup.md](project_setup.md).
