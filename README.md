# cwnt.io management
Repo for management, issues, docs, etc...

<!-- toc GFM -->

+ [unorganized issues](#unorganized-issues)
+ [Scrum / Agile](#scrum--agile)
+ [Symlinks](#symlinks)
+ [Project Definition](#project-definition)

<!-- toc -->

# unorganized issues

- order issues inside kanban board


# Scrum / Agile

- Stories, also called “user stories,” are short requirements or requests written from the perspective of an end user.
- Epics are large bodies of work that can be broken down into a number of smaller tasks (called stories).
- Initiatives are collections of epics that drive toward a common goal.

[Stories, epics, and initiatives](https://www.atlassian.com/agile/project-management/epics-stories-themes)

```
.
├── epics
├── initiatives
├── issues
├── projects
│  └── popcorn
│     └── kanban
│        ├── 0-backlog
│        ├── 1-todo
│        ├── 2-doing
│        ├── 3-staging
│        └── 4-closed
└── README.md
```

# Symlinks

[How to find and remove broken symlinks on Linux ](https://www.networkworld.com/article/3546252/how-to-find-and-remove-broken-symlinks-on-linux.html)
- When symlinks get broken
- Finding broken symlinks

```bash
# all symlinks
fd -tl
find . -type l
# just broken/dead
fd -L -tl # fd --follow --type symlink
find . -type l ! -exec test -e {}
find . -xtype l
```

- What to do with broken symlinks

```bash
find . -xtype l 2>/dev/null -exec rm {} \;
# or
rm ref1
ln -s /apps/data/newfile ref1
```

- fd print destination of link

```bash
fd -tl -x readlink
fd -L -tl -x readlink
```

# Project Definition

[board picture]('./media/signal-2023-09-01-172412_002.jpeg')
