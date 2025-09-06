# `changesets-action-playground-pat`

Trying to have changeset PR triggering CI workflows on creation and on PR update.

1. Create a Personal Access token with the following permissions
   - contents: read & write
   - metadata: should be added after contents
   - pull requests: read & write

2. Store the personal access token as a repository action secret

3. Setup git config with valid credentials

   ```sh
   git config --global user.name '...'
   git config --global user.email '...'
   ```

4. Checkout the repo via actions/checkout with `persist-credentials: false`

   ```yml
   - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
          persist-credentials: false 
   ```

5. Run changeset with `setupGitUser: false`

   ```yml
    - name: Create Release Pull Request or Publish to npm
      id: changesets
      uses: changesets/action@v1
      with:
        # other options
        setupGitUser: false
      env:
        GITHUB_TOKEN: ${{ secrets.CHANGESETS_PR_TOKEN }} # Your personal access token goes here
        NPM_TOKEN: ${{ secrets.NPM_TOKEN }}
   ```
