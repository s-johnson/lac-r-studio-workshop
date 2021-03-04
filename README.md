# `shinytest` Example

An example application (OpenFDA Adverse Events Data) for
using and illustrating how `shinytest` works.

## How to use this repository

- Fork the repository for yourself
- Check it out locally to see how `shinytest` works
- Change the GitHub actions as discussed below
    - Change the Connect URL to your own Connect URL
    - Add your own `CONNECT_API_KEY` secret
- Make "breaking changes" to the application and see the tests fail
- Run the tests interactively yourself
- Send a PR to _your own_ `main` branch (within your fork)
- Use or improve this pattern for your own work!!

## Run `shinytest`

In order to run `shinytest`, you need to:

- Install dependencies with `renv::restore()`
- Activate the renv environmetn: `renv::activate()`
- Run tests with `shinytest::testApp()`
- If there are differences, view the differences with
`shinytest::viewTestDiff(testnames = "mytest")` (for the `mytest` test)

## CI testing with `shinytest` and GitHub Actions

- Create a
[`.github/workflows/run-shinytest.yaml`](./.github/workflows/run-shinytest.yaml)
file
- If the tests succeed, the workflow run will pass
- If the tests differ or fail, the workflow run will fail
- To review the results directly, you have to download the build artifacts
- Alternatively, since tests are failing, it means that something about the
application has changed. Tests may need to be updated (or code fixed) to address
the changes. To do this, you can run the tests locally or address any code
changes necessary

## CI Deployment to RStudio Connect

### Using GitHub Actions

- The approach we take presumes a `manifest.json`. This _could_ be generated by
a GitHub action, but instead we generate during our dev work using
`rsconnect::writeManifest()`

- Then create a
[`.github/workflows/rstudio-connect.yaml`](./.github/workflows/rstudio-connect.yaml)
file

- Specify your `url: ` (should be your RStudio Connect URL)

- In GitHub Actions on your repo, set the `CONNECT_API_KEY` secret
   - Go to the repository on GitHub
   - Navigate to Settings > Secrets
   - Create a "New Repository Secret" with an API key

### Using git-backed deployment

RStudio Connect supports a "pull-based" git-backed deployment and polling.

In this mode, Connect will watch a branch of your repository and deploy any new
commits that it detects, depending upon a server-wide polling interval.

[You can read more about the process here](https://docs.rstudio.com/connect/user/git-backed/)

## Future Development Work (for developers)

Our goal is to continue improving this process and making it easier! Some
current ideas of next steps. Your feedback, contribution, and ideas are welcomed
and encouraged!

- Make sure all links / etc. create a usable workflow
- Make GitHub actions easier to extend, add functionality (i.e. content tags on Connect, etc.)
- Add `shinytest` example actions to `usethis` to follow the
`usethis::use_github_action()` pattern
- Make example `shinytest` actions that integrate more effectively with RStudio
Connect for reviewing results, etc.
- Fix the Windows shinytest running (currently fails)
- Make system deps (on Ubuntu) run more effectively / dynamically ([r-lib
patterns](https://github.com/r-lib/actions) orient mostly around packages)
- Package up more of these items as re-usable components to simplify the user workflows
- Better patterns around using / accepting test changes, artifacts, etc.
- Figure out cross-operating-system compatibility issues

## Future Exploration (for users)

Some other areas you can explore for your own apps / assets:

- Only deploy to Connect if tests complete successfully
- Change configuration of what tests run where / etc.
