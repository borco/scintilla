# Scintilla unofficial automatic mirror

This is an **unofficial** automatic mirror for the <http://hg.code.sf.net/p/scintilla/code> mercurial repo of the [Scintilla](https://www.scintilla.org/) project.

* uses [git-cinnabar](https://github.com/glandium/git-cinnabar) to interact with the scintilla mercurial repo
* the [master](https://github.com/missdeer/scintilla/tree/master) branch from this repo corresponds to [default](http://hg.code.sf.net/p/scintilla/code/file/default) branch from the scintilla mercurial repo
* the [tags](http://hg.code.sf.net/p/scintilla/code/tags) from the scintilla mercurial repo are mirrored verbatim
* the mirroring code is on the `mirror` branch from this repo

This repo is based on the code from the <https://github.com/missdeer/scintilla> project.

---

## For mirror maintainers

### Configuring the secrets

Every time the mirror action runs, it pushes the code and tags from the official repo into this mirror repo. In order to be able to do this, the action uses the `GH_TOKEN_SCINTILLA` secret that contains a *token* configured to allow access to the repo code.

#### Define a personal access token

* go to your *Settings > Developer settings > Personal access tokens > Fine-grained tokens*
* click the `Generate new token` (or select the existing token, if you want to update it)
* set the new token:
  * name: `GH_TOKEN_SCINTILLA`
    * the *name* can be anything, but it is easier to maintain if we use the same name as the secret and have them unique
  * expiration: `No expiration`
  * description: `Token to push to https://github.com/borco/scintilla`
    * the description can be empty, but it is easier to have something that explains its purpose
  * repository access:
    * check `Only select repositories`
    * select the current repo from the `Select repositories` dropdown
  * permissions:
    *  select `Read and write` for the `Codespaces` repository permission
    *  selecting the above will automatically give `Read-only` access to `Metadata` repository permission
    *  no other permissions are required
  * click the `Generate token` to generate the token
  * save the token value somewhere safe

#### Use the token for mirroring

* go to the *Project > Settings > General > Secrets and variables > Actions*
* click on `New repository secret` to create a new secret or click the *pen* icon to edit the existing one
  * name: `GH_TOKEN_SCINTILLA` (must match the secret name used in `.github/workflows/sync.yml`)
  * secret: `***` (set it to the value saved when you've created or updated the access token)
