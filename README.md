# Create Theme Preview

This GitHub action creates a preview of a pull request for a Shopify store. It makes it easier to see the changes made in a pull request before they are merged.

The action has the following steps:

1. Get the current date and time
2. Create a comment on the pull request for the loading state with a table containing the name of the store, the status of the preview creation, and the date and time of the action
3. Check out the current pull request
4. Set up Node.js and Ruby
5. Install the Shopify CLI
6. Use the Shopify CLI to create the preview and save the returned preview link in an output object
7. Update the table to display the preview links
8. If any of the previous steps fail, create a comment on the pull request with an error message


## Inputs
| Name | Description | Example |
| ---- | ----------- | ------- |
| `shopify_flag_store` | Your Store URL | `your-store.myshopify.com` | 
| `shopify_cli_theme_token` | Password generated from [Theme Access App](https://shopify.dev/themes/tools/theme-access) | `shptka_7e95eace43t00be7f9f8612325212805` |


## Example usage

### Create a preview link and add it to the comment
The action searches for the `!preview` keyword in a pull request comment and replaces the whole comment with a table that contains a preview and editor link. You can change this keyword to filter for a different string in the pull request comments.

```yaml
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
      - uses: DavidPotato/create-preview@v5
        with:
          shopify_flag_store: 'your-store.myshopify.com'
          shopify_cli_theme_token: 'shopify_cli_theme_token'
```
> Just write a comment like this:
![image](https://user-images.githubusercontent.com/77160493/206173680-5e960d83-807d-4205-9d25-b962e6a30091.png)

> After the action finished loading the table with the preview links should look like this:
![image](https://user-images.githubusercontent.com/77160493/206173320-c68ae50a-5afa-48d7-bb70-690612cd1d58.png)


