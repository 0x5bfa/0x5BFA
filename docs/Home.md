> [!IMPORTANT]
> This docs is not yet for public and after all specs mentioned get implemented, this wiki will be published onto our website.
> **Do NOT copy or redistribute modified versions.**

## Preface

We'll be explaining how we built the current simple architecture. This enables new contributors to easily join our community and participate in Files development.

## Basic architecture

Excluding `Sidebar`, all controls of them below are `UserControl`s to pass arbitrary DP. While associated `FolderBrowser` is created when a tab created and that tab has its `FolderBrowser` instance, other controls, such as `InfoPane` and `Toolbar` in `Sidebar.Content` are single-instantiated and receive the current focused `FolderBrowser`.

*Figure 1. MainPage's XAML structure*
![MainPage XAML Structure](https://github.com/user-attachments/assets/f0a96d6f-32d2-4183-a3aa-e41e0f782351)
