# .github/rulesets

> [!NOTE]
> See [this GitHub documentation about rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets 'https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets') for reference.

- [Ruleset Files](#ruleset-files)
    - [All Branches Deletion Protection](#all-branches-deletion-protection)
    - [All Branches Force Push Protection](#all-branches-force-push-protection)
    - [Main Branch Deletion Protection](#main-branch-deletion-protection)
    - [Main Branch Protection](#main-branch-protection)
    - [All Tags Protection](#all-tags-protection)
- [Importing Ruleset Files](#importing-ruleset-files)

# Ruleset Files

> [!IMPORTANT]
> GitHub does not automatically read or enforce these `.json` files just by committing them to the repository.
> They must be manually imported via the GitHub Settings UI.
> See [the "Importing Ruleset Files" section](#importing-ruleset-files '#importing-ruleset-files') for reference.

## All Branches Deletion Protection

- Applies to all branches

```JSON
"include": ["~ALL"]
```

- Prevents anyone from deleting a branch
    - Except for repository administrators

```JSON
"type": "deletion"
// except for repository administrators
"actor_id": 5
```

> [!NOTE]
> See [`all-branches-deletion-protection.json`](./all-branches-deletion-protection.json './all-branches-deletion-protection.json') for reference.

## All Branches Force Push Protection

- Applies to all branches

```JSON
"include": ["~ALL"]
```

- Prevents force-pushes on all branches
    - Except for repository administrators and explicitly designated bypass actors (teams/users)

```JSON
"type": "non_fast_forward"
// except for repository administrators and designated bypass actors
"actor_id": 5
```

> [!NOTE]
> See [`all-branches-force-push-protection.json`](./all-branches-force-push-protection.json './all-branches-force-push-protection.json') for reference.

## Main Branch Deletion Protection

- Applies exclusively to the `main` branch

```JSON
"include": ["refs/heads/main"]
```

- Prevents anyone from deleting the `main` branch
    - Absolute restriction with zero exceptions
    - Blocks repository administrators and owners completely

```JSON
"type": "deletion"
// bypass_actors is empty
"bypass_actors": []
```

> [!NOTE]
> See [`main-branch-deletion-protection.json`](./main-branch-deletion-protection.json './main-branch-deletion-protection.json') for reference.

## Main Branch Protection

- Applies exclusively to the `main` branch

```JSON
"include": ["refs/heads/main"]
```

- Prevents force-pushes on the `main` branch
    - Except for repository administrators

```JSON
"type": "non_fast_forward"
// except for repository administrators
"actor_id": 5
```

- Requires a linear history
    - Blocking standard merge commits

```JSON
"type": "required_linear_history"
```

- Enforces that all changes to `main` must go through a pull request
    - Requiring at least 1 approval
    - Dismissing stale approvals on new pushes
    - Requiring all review threads to be resolved
    - Allowing direct push bypass for admins

```JSON
"type": "pull_request"
"required_approving_review_count": 1
"dismiss_stale_reviews_on_push": true
"require_review_thread_resolution": true
// allowing direct push bypass for admins
"actor_id": 5
```

- Mandates a code owner's approval on `main` pull requests

```JSON
"require_code_owner_review": true
```

- Requires passing status checks on pull requests targeted at `main`

```JSON
"type": "required_status_checks"
"context": "CI"
"context": "E2E"
```

> [!NOTE]
> See [`main-branch-protection.json`](./main-branch-protection.json './main-branch-protection.json') for reference.

## All Tags Protection

- Applies to all tags

```JSON
"include": ["~ALL"]
```

- Prevents anyone from deleting or modifying an existing tag
    - Except for repository administrators

```JSON
"type": "deletion"
"type": "update"
// except for repository administrators
"actor_id": 5
```

> [!NOTE]
> See [`all-tags-protection.json`](./all-tags-protection.json './all-tags-protection.json') for reference.

## Importing Ruleset Files

To actively enforce these rules on this repository, follow the steps described in [this "Importing a ruleset" GitHub documentation](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/managing-rulesets-for-a-repository#importing-a-ruleset 'https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/managing-rulesets-for-a-repository#importing-a-ruleset').
