### Configuration

- Generate a fresh SSH keypair
- Add the public key as a write-access deploy key to the repo
- Create a new secret called `DEPLOY_KEY` with the private key in PEM format

#### Env vars worth setting:

- `GIT_USER_NAME` - username for automated commit user
- `GIT_USER_EMAIL` - email for automated commit user
- `PULL_REQUEST_TITLE` - name of the pull request to create

### Notes
 
- We hardcode Github's SSH pubkeys into our known_hosts for security reasons
    - these are gotten via: `ssh-keyscan github.com`
    - For unknown reasons this no longer works, temporary fix is to ignore host keys
        - Noted with a FIXME
- Expects `develop` branch to exist already by convention
    - provides a sane error message if an expected branch does not exist

#### Creates pull requests as follows:

- If we’re on master:
    - Open PRs with changes from head branch master onto base branches matching:
        - 'release/.*'
        - 'hotfix/.*'
- If we’re on a branch matching 'release\/.*':
    - Open PRs from each release branch to develop
- If we’re on develop:
    - Open PRs with changes from head branch develop onto base branches matching 'sprint/.*'
