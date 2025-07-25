---
tags:
  - Status200
---


# 🌱 **Status 200 Contribution Guide**

Thank you for your interest in contributing to **Status 200**! Your contributions will help this digital garden grow and become an even more valuable resource for tech enthusiasts worldwide. Follow the steps below to get started.

## 🚀 **How to Contribute?**

Here's a detailed guide on how you can start contributing to the Status 200 Digital Garden:

### 1. **Fork the Repository**

A fork is your personal copy of the original project. You’ll make changes in your fork and then suggest those changes be added to the main project. Here’s how to fork the repository:

1. Go to the [Status 200 repository](https://github.com/sarthakchandajkar/status200).
2. Click the **Fork** button at the top right of the repository page. This creates a copy of the repository in your GitHub account.

> **Tip:** If you are unfamiliar with forking a repository, check out the official GitHub documentation on the concept [**here**](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo).

### 2. **Clone Your Forked Repository**

Cloning means downloading a copy of the repository to your computer so you can work on it locally.

1. **Open Your Terminal**: If you’re using Windows, you can use Command Prompt or PowerShell. On macOS or Linux, use the built-in Terminal. Alternatively, you can use the terminal in [Visual Studio Code (VSCode)](https://code.visualstudio.com/) if you have it installed.
    
2. **Copy the Repository URL**: Go to your forked repository on GitHub. Click the green **Code** button, then copy the URL (it should look like `https://github.com/your-username/status200.git`).
    
3. **Run the Clone Command**: In your terminal, type the following command and press **Enter**:


```
git clone https://github.com/your-username/status200.git
```

4. **Navigate to the Project Folder**: After cloning, move into the project folder:
```
cd status200
```

### 3. **Install Quartz Locally**

Quartz is an open-source digital garden framework that allows you to publish your notes as a website. It’s the backbone of Status200, helping us organize and display content in a clear, interconnected way. With Quartz, your contributions are automatically formatted and linked within the larger structure of the garden, making it easier for users to navigate the knowledge.

You can learn more about Quartz in the [Quartz Documentation](https://quartz.jzhao.xyz).

Quartz is already included in the repository. To install all necessary dependencies, simply run:

```
npm i
```

>**Note:** Make sure your Node.js and npm versions are compatible with Quartz. Refer to the  [Quartz Documentation](https://quartz.jzhao.xyz). for the specific version requirements.

### 4. **Create a New Branch**

In Git, a branch is like a separate workspace where you can make changes without affecting the main project. 

Creating a branch helps keep your work organized and makes it easier to merge changes later. You avoid conflicts by keeping your changes separate from others.

Here’s how to create one:

```
git checkout -b your-branch-name
```

Replace `your-branch-name` with a descriptive name related to your contribution.

### 5. **Open the Cloned Folder as a Vault in Obsidian**

Obsidian is a note-taking app we use to write and organize content. Here’s how to set it up:

1. **Download and Install Obsidian**: If you don’t already have it, download Obsidian from [here](https://obsidian.md/).
    
2. **Open the Cloned Folder as a Vault**:
    
    - Open Obsidian.
    - On the main screen, choose **Open Folder as Vault**.
    - Navigate to the folder where you cloned the repository (likely named `status200`) and select it.

### 6. **Install the Templater Plugin in Obsidian**

To maintain consistency across all contributions, we use a pre-defined template that everyone follows. This is managed using the **Templater** plugin in Obsidian.

1. **Install the Templater Plugin**:
    
    - Go to **Settings** in Obsidian.
    - Click on **Community Plugins** and search for “Templater”.
    - Install and enable the Templater plugin

> [!NOTE]
 	Note: If this is your first time using Obsidian, you might need to enable community plugins as prompted. After enabling them, it’s recommended to close and reopen Obsidian.
	
2. **Use the Template**:
    
    - Right-click on the `content` folder in Obsidian.
    - Select **Create new note from template**.
    - When prompted, choose the template called `page` from the `templates` folder. `page` is the default template that is present in the template folder of the repository. It is the default format used by Quartz

This ensures your note follows the structure and formatting common to the rest of the digital garden.
### 7. **Add Your Content**

Now, you can start adding your notes, roadmaps, study materials, or personal experiences. Add your content inside the `content` folder of the repository. 

```
cd content
```

You can organize your content into subfolders for different topics, such as:

`- content/`   
`- software-development/`     
`- ai-ml/`     
`- data-science/`  
`- solutions-architecture/`

Feel free to use Markdown for your notes, and make sure to link related topics using relative paths like:


```
[Learn more about AI/ML](../ai-ml/intro.md)
```

### 8 **Create Backlinks to Connect Ideas**

To make **Status 200** more interconnected and easy to navigate, we strongly encourage you to create backlinks between related ideas and topics. This enhances the garden’s utility by allowing users to seamlessly explore connected concepts.

In Obsidian, you can create backlinks by enclosing the name of another note in double square brackets:

```
[[Data Structures]]
```

Use these links generously to connect ideas, build a web of knowledge, and create a richer learning experience for everyone!
### 9. **Commit , Push and  Publish Your Changes**

Once you’re happy with your additions, commit and push your changes:

```
git add . 
git commit -m "Added new content on AI/ML" 
git push origin your-branch-name
```

Then, you can sync the content to upload it to your repository. This is a helper command that will do the initial push of your content to your repository.

```
npx quartz sync
```

>For a more detailed explanation on the helper commands, check out the [Setting up your Github Repository](https://quartz.jzhao.xyz/setting-up-your-GitHub-repository) page in the Quartz Documentation

**Publish Your Branch**: If this is your first time pushing this branch, GitHub may ask you to publish it:

```
git push --set-upstream origin your-branch-name
```

The changes should now be uploaded to your fork on Github

### 10. **Create a Pull Request**

After pushing your changes to your forked repository:

1. Go to your fork on GitHub.
2. Click **Compare & pull request**.
3. Write a brief description of the changes you made and submit the pull request.

We’ll review your submission, and if everything looks good, your content will be merged into the main `v4` branch!

### 11. **Keep Exploring and Contributing**

Remember, the garden is constantly evolving. Keep contributing as you learn and grow, and encourage others to do the same!

## 🌟 **Need Help?**

If you run into any issues or have questions, feel free to reach out. You can open an issue in the repository, or contact us directly.

Happy contributing, and welcome to the Status 200 community!