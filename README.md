<a href="https://reporacers.com/" taarget="_blank">
  <img src="https://github.com/repo-racers/.github/blob/main/profile/repo-racers.svg" alt="Repo Raacers" width="600px"/>
</a>

This repository is included in our open-source Pro Support service which offers an efficient solution for managing popular GitHub Actions dependencies with ease:

🙌 forked from [jpoehnelt/secrets-sync-action](https://github.com/jpoehnelt/secrets-sync-action)

<details>

<summary>What is Open-Source Pro Support?</summary>

Open-Source Pro Support is a comprehensive service designed to streamline your workflow by providing:

- **Customized Forks:** We create public forks of popular GitHub Actions, ensuring you have access to the latest features and fixes.
  
- **Dedicated Technical Support:** Say goodbye to the hassle of managing multiple open-source dependencies. With our service, you have a single point of contact for all your support needs. Reach out to us on our [Discord](https://discord.com/channels/1229786735161118882/1229786735161118885) server, and our team of experts will be ready to assist you.
  
- **Priority Fixes:** Experience seamless issue resolution with our priority fix service. If you encounter any issues with our forks, we prioritize fixing them promptly to minimize disruptions to your workflow.
  
- **Community Contribution:** We believe in giving back to the open-source community. When we fix issues in our forks, we handle creating pull requests to the original authors, ensuring that the entire community benefits from the improvements.

</details>

<details>

<summary>How It Works</summary>


1. **Choose Our Fork:** Instead of referencing popular GitHub Actions repositories directly, simply reference this repository in your workflow.
   
2. **Enjoy Dedicated Support:** If you encounter any issues or need assistance, reach out to us on our [Discord](https://discord.com/channels/1229786735161118882/1229786735161118885) server. Our team will be happy to help you promptly.
   
3. **Benefit from Priority Fixes:** Experience seamless issue resolution with our priority fix service. We prioritize fixing issues in our forks to ensure smooth operation for your projects.
   
4. **Contribute to the Community:** Rest assured that when we fix issues in our forks, we contribute back to the original repositories, benefiting the entire open-source community.

*Not Your Thing?*

We don't want to get in between you and the community. If you want to handle forking and submitting a pull request yourself, that's awesome.

However, feel free to reach out to us on [Discord](https://discord.com/channels/1229786735161118882/1229786735161118885) anyway if you need any help and advice in doing so.

:heart: [open-source](https://opensource.org/)

</details>

---

# Secrets Sync Action

A Github Action that can sync secrets from one repository to many others. This action allows a maintainer to define and rotate secrets in a single repository and have them synced to all other repositories in the Github organization or beyond. Secrets do not need to be sensitive and could also be specific build settings that would apply to all repositories and become available to all actions. Regex is used to select the secrets and the repositories. Exclude is currently not supported and it is recommended to use a bot user if possible.

## Inputs

### `github_token`

**Required**, Token to use to get repos and write secrets. `${{secrets.GITHUB_TOKEN}}` will **not** work as it does not have the necessary scope for other repositories. This token should have the full "repo" scope. In older instances of GitHub, a fine-grained token may not support the required GraphQL API and a "Classic" personal access token would be required. As this is deprecated, please try a fine-grained token first.

### `repositories`

**Required**, Newline delimited regex expressions to select repositories. Repositories are limited to those in which the token user is an owner or collaborator. Set `repositories_list_regex` to `False` to use a hardcoded list of repositories. Archived repositories will be ignored.

### `github_api_url`

Override default GitHub API URL. When not provided, the action will attempt to use an environment variable provided by the GitHub Action runner environment defaults.

### `repositories_list_regex`

If this value is `true` (default), the action will find all repositories available to the token user and filter based upon the regex provided. If it is `false`, it is expected that `repositories` will be a newline delimited list in the form of org/name.

### `secrets`

**Required**, Newline delimited regex expressions to select values from `process.env`. Use the action env to pass secrets from the repository in which this action runs with the `env` attribute of the step.

### `retries`

The number of retries to attempt when making Github calls when triggering rate limits or abuse limits. Defaults to 3.

### `concurrency`

The number of allowed concurrent calls to the set secret endpoint. Lower this number to avoid abuse limits. Defaults to 10.

### `dry_run`

Run everything except for secret create and update functionality.

### `delete`

When set to `true`, the action will find and delete the selected secrets from repositories. Defaults to `false`.

### `environment`

If this value is set to the name of a valid environment in the target repositories, the action will not set repository secrets but instead only set environment secrets for the specified environment. When not set, will set repository secrets only. Only works if `target` is set to `actions` (default).

### `target`

Target where secrets should be stored: `actions` (default), `codespaces` or `dependabot`.

## Usage

```yaml
uses: repo-racers/secrets-sync-action@[insert version or commit]
  with:
    SECRETS: |
      ^FOO$
      ^GITHUB_.*
    REPOSITORIES: |
      ${{github.repository}}
    DRY_RUN: true
    GITHUB_TOKEN: ${{ secrets.PERSONAL_GITHUB_TOKEN_CLASSIC }}
    GITHUB_API_URL: ${{ secrets.CUSTOM_GITHUB_API_URL }}
    CONCURRENCY: 10
  env:
    FOO: ${{github.run_id}}
    FOOBAR: BAZ
```

See the workflows in this repository for another example.

---

> [!TIP]
> For support with this repo and many other open-source projects, visit us at https://reporacers.com/ and join us on  [Discord](https://discord.com/channels/1229786735161118882/1229786735161118885).
