# API-Integration-Pagination 
 
A small Go example that fetches all GitHub repository issues updated since a given time.

## Pagination fix

`FetchIssues` follows GitHub's `Link` header by using `resp.NextPage` instead of assuming that a page is the last page when it contains fewer issues than `PerPage`.

This matters when the GitHub API returns a short page while a later page is still available, including requests that use the `since` filter.

## Run

Set a GitHub token if you want to run the demo against GitHub:

```bash
export GITHUB_TOKEN=your_token
go run main.go
```

On Windows PowerShell:

```powershell
$env:GITHUB_TOKEN="your_token"
go run main.go
```

## Test

Run the unit tests:

```bash
go test ./...
```

The test suite includes a regression test where a page contains fewer issues than `PerPage` but GitHub reports another page through `Link`.
