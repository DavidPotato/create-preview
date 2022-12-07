# Create Theme Preview

This GitHub action creates a preview of a pull request for a Shopify store. 

It has the following steps:

1. Get the current date and time
2. Create a comment on the pull request for the loading state with a table containing the name of the store, the status of the preview creation, and the date and time of the action
3. Check out the current pull request
4. Set up Node.js and Ruby
5. Install the Shopify CLI
6. Use the Shopify CLI to create the preview and save the returned preview link in an output object
7. Update the table to display the preview links
8. If any of the previous steps fail, create a comment on the pull request with an error message

This action makes it easier to see the changes made in a pull request before they are merged.

## Inputs

- `shopify_flag_store`: Store URL, like `your-store.myshopify.com`
- `shopify_cli_theme_token`: Password generated from [Theme Access App](https://shopify.dev/themes/tools/theme-access)


## Example usage

# Create a preview link and add it to the comment
The action searches for the `!preview` keyword in a pull request comment and replaces it with a table that contains a preview and editor link.

```
run-name: Create Theme Preview by @${{ github.actor }}
on:
  issue_comment:      
    types: [created]    
jobs:                   
  deploy:
    name: Preview
    runs-on: ubuntu-latest
    if: contains(github.event.comment.body, '!preview')
    steps:
      - name: EXECUTE COMPOSITE ACTION
        uses: DavidPotato/create-preview@v5
        with:
          shopify_flag_store: '*your-store.myshopify.com*'
          shopify_cli_theme_token: '*shopify_cli_theme_token*'
```