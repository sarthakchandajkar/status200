# 🌱 **Status 200 Contribution Guide**

Thank you for your interest in contributing to **Status 200**! Your contributions will help this digital garden grow and become an even more valuable resource for tech enthusiasts worldwide. Follow the steps below to get started.

## 🚀 **How to Contribute?**

To contribute, all you need to do is clone the repository, install Quartz, and start adding your files to the content folder. Here's a detailed guide:

### 1. **Fork the Repository**

Before cloning, you need to fork the **Status 200** repository to your own GitHub account.

1. Go to the [Status 200 repository](https://github.com/sarthakchandajkar/status200).
2. Click the **Fork** button at the top right of the repository page. This creates a copy of the repository in your GitHub account.

### 2. **Clone Your Forked Repository**

Now, clone your forked repository to your local machine:

```git clone https://github.com/your-username/status-200.git
```

### 3. **Create a New Branch**

To avoid making changes directly to the `v4` branch, create a new branch for your contributions:

```
git checkout -b your-branch-name
```

Replace `your-branch-name` with a descriptive name related to your contribution.
### 4. **Install Quartz Locally**

Quartz is the tool we use to build and host this digital garden. Follow the steps below to install it:

1. **Navigate to the repository:**

```
cd status-200
```

2. **Install Quartz:**

```
npm i
```


For more detailed instructions on installing Quartz, visit the official [Quartz Documentation](https://quartz.jzhao.xyz).

### 5. **Open the Cloned Folder as a Vault in Obsidian**

To add content efficiently, open the cloned repository folder as a vault in Obsidian:

1. Open Obsidian.
2. Select **Open Folder as Vault**.
3. Navigate to the folder where you cloned the repository (`status-200`) and select it.

Now, you can directly create, edit, and organize your notes in Obsidian.

### 6. **Add Your Content**

Once Quartz is installed, you can start adding your notes, roadmaps, study materials, or personal experiences. Add your content inside the `content` folder of the repository. 

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

### 7. **Create Backlinks to Connect Ideas**

To make **Status 200** more interconnected and easy to navigate, we strongly encourage you to create backlinks between related ideas and topics. This enhances the garden’s utility by allowing users to seamlessly explore connected concepts.

In Obsidian, you can create backlinks by enclosing the name of another note in double square brackets:

```
[[Data Structures]]
```

Use these links generously to connect ideas, build a web of knowledge, and create a richer learning experience for everyone!
### 8. **Commit and Push Your Changes**

Once you’re happy with your additions, commit and push your changes:

```
git add . 
git commit -m "Added new content on AI/ML" 
git push origin your-branch-name
```

### 9. **Create a Pull Request**

After pushing your changes to your forked repository:

1. Go to your fork on GitHub.
2. Click **Compare & pull request**.
3. Write a brief description of the changes you made and submit the pull request.

We’ll review it, and once approved, your content will be merged into the main repository!

### 10. **Keep Exploring and Contributing**

Remember, the garden is constantly evolving. Keep contributing as you learn and grow, and encourage others to do the same!

## 🌟 **Need Help?**

If you run into any issues or have questions, feel free to reach out. You can open an issue in the repository, or contact us directly.

Happy contributing, and welcome to the Status 200 community!