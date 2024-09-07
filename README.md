---

# Hashnode Publishing via GitHub - Breachforce Checklist

This README serves as a reference guide for publishing articles from GitHub to Hashnode, ensuring smooth and error-free publication.

## 1. Naming Convention for Files
- **File Naming**: 
  - Use **lowercase** letters only.
  - The file name should be **a single word** with **hyphens (-)** as separators (no spaces, underscores, or other characters).
  - The file must end with a **`.md`** extension.
- **URL Consideration**: 
  - The name of the file becomes part of the article URL on Hashnode, so choose a meaningful name.

## 2. File Placement
- Ensure the file is placed at the **root directory** of the GitHub repository, not inside any subfolder.

## 3. First Push Success
- If the article is not successfully published from GitHub on the first attempt:
  - **Delete the file** from GitHub.
  - Rectify the issue and re-upload it, as subsequent changes to the file will not reflect on Hashnode.

## 4. Publishing Team Setup

- If another team member is publishing the blog, ensure that:
  - The member is added to the **Hashnode blog team**.
  - Their **Hashnode user ID** must be included in the code (e.g., `65c1234abcd12a3a3ef3b943`).
  
- **Fetch User ID**:
  1. The user must have an account on Hashnode.
  2. Go to the user’s **Hashnode profile page**. The URL should look like:  
     `https://hashnode.com/@JohnDoe`  
     (Replace `JohnDoe` with the actual username).
  3. Extract the username from the URL (in this case, `JohnDoe`).
  4. Visit Hashnode’s public **GraphQL Playground** at:  
     [https://gql.hashnode.com/](https://gql.hashnode.com/)
  5. Run the following GraphQL query by replacing `"JohnDoe"` with the actual username:
     ```graphql
     query GetUser {
       user(username: "JohnDoe") {
         id
         name
       }
     }
     ```
  6. From the query response, use the `id` value you retrieve (e.g., `65c1234abcd12a3a3ef3b943`).
  7. Pass this **user ID** into the `.md` file that you are pushing to GitHub for the article to be published correctly.

## 5. Template Cleanup
- **Remove all comments (`#`)** from the markdown file before committing to GitHub, as they will prevent the article from being published.

## 6. Series Creation and Navbar Update
- **New Series**:
  - Create a new series and add relevant content.
  - Navigate to **Navbar > Add item**, and:
    - Set a label.
    - Choose **Series** as the type.
  - The series will now appear in the navbar.

## 7. Syncing Articles (GitHub & Hashnode UI)
- **Two-way sync**: Changes made via the Hashnode UI do **not sync back** to GitHub. To enable two-way sync, a middleware setup is required.
- Workflow:
  - **GitHub to Hashnode**: Submit the final article from GitHub.
  - **Touch-ups**: Update via the Hashnode UI if needed, but this **won't affect** the GitHub version.

## 8. Deploying Another File
- If a new file is deployed:
  - **Does it change the previous article on Hashnode?** → No.
  - **Does it update the article on GitHub?** → No.
  
  Subsequent posts may fail after making changes directly from the Hashnode UI. If this happens:
  - **Roll back** to the successful build from GitHub.

## 9. Cover Images
- For cover images:
  - **Drag and drop** the image in the GitHub UI.
  - Use the **URL** of the image as a string in the markdown file.

## 10. Getting the Series ID
- To get the **Series ID**:
  - Go to **Account Settings** where the series is created.
  - Open the **Network tab** in the browser developer tools.
  - Find the **POST** call to `gql.hashnode.com`, and look in the response for the series ID.
  - The series id for Notes here would be `66db123abc123abc123e89d`  
  
  Example:
  ```json
  {
    "data": {
        "publication": {
            "id": "65b61123abc123abc123f385",
            "seriesList": {
                "edges": [
                    {
                        "node": {
                            "id": "66db123abc123abc123e89d",
                            "name": "Notes",
                            "cuid": "cm0rc32123abc123abc1239z2",
                            "slug": "notes",
                            "sortOrder": "dsc"
                        }
                    }
                ]
            }
        }
    }
  }
  ```

---
