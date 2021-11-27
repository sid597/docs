# Feature Reference

## App Toolbar

The app toolbar is home to many of the controls in Athens. From left to right:
- [DB Picker](#db-picker)
- [Left Sidebar](#left-sidebar)
- [Daily Notes](#daily-notes)
- [All Pages](#all-pages)
- [Graph Visualization](#graph-visualization)
- [All Pages](#all-pages)
- [Athena](#athena)
- [Import](#import)
- [Settings](#settings)
- [Dark Mode](#dark-mode)
- [Help Menu](#help-menu)
- [Right Sidebar](#right-sidebar)

## Left Sidebar

The left sidebar contains your list of favorites. (link to making a favorite)

The bottom contains your Athens client version number.

## Right Sidebar

## Backups

At Athens, we fundamentally believe in data ownership and data privacy. It is from this belief that our backup system has been implemented. The primary goal of our backup system is to make it possible to revert your data back to any point in time so that there is _zero_ room for data loss due to corruption and other formatting issues.

Restoring from Backups

Backups in Athens are stored in a `.bkp` format which is easy to restore from. They are named with a [Unix timestamp](https://en.wikipedia.org/wiki/Unix_time) based on when they were created.

Restoring from a `.bkp` file is a five-step process.

Locate your database folder

Backups in Athens are stored in your main DB folder and have a `.bkp` file extension. To locate your database folder, in the Athens app, click the database icon on the toolbar and you will see the current location of your database. In this folder, you will see your backup files.

![](/img/gitbook/image-4.png)

Relocate your `index.transit` file

Before we proceed to the next step, locate your current `index.transit` file and relocate it to another folder.

![](/img/gitbook/123552515-160cc780-d794-11eb-961d-8c277b3f632e-1.gif)

Locate the backup file you want to restore from

Once you are in the folder, find a file with a creation time that corresponds to the state of your database you would like to revert to. For instance, let's say you want to restore my DB to where it was on the night of June 6th. In this case, you find a `.bkp` file with a creation time around that specific time. You can also use a [Unix time converter](https://time.is/Unix_time_converter) to figure out when Athens created a `.bkp` file.

Rename the backup file

At this point, rename the selected `.bkp` file to `index.transit`.

![](/img/gitbook/123552503-0ab99c00-d794-11eb-938a-14fe80200184.gif)

Open the new file in Athens

![](/img/gitbook/image-5.png)

Reopen Athens, click the database icon once again and make sure you are on the **Open** pane. Proceed to click the open button and navigate to the newly created \`index.transit\` file. You have now reverted to a backup! All new backups will be created from this file and changes made to your DB will also reflect in the new `index.transit` file.

Frequency of backups

You can set your desired backup and auto save frequency in the settings page. By default, Athens saves a copy of your database every 15 seconds into your main folder.

Best practices

As Athens currently doesn't automatically delete your old backups, it becomes important to periodically clear out your folder in order to prevent it from taking too much space on your hard drive. The lower your auto save interval, the more frequently you should undertake this activity.

Additionally, because the backups are locally stored \(for the moment\), it makes sense to periodically backup the folder to a cloud service like Dropbox or Google Drive.

## Import

To download a `.edn` file from Roam Research, visit your Roam graph and click on the three doc symbol **⋯** in the top bar, then **Export All**. Choose **EDN** from the Export Format dropdown, then click **Export All**.

You'll download a `.zip` file, which you need to open/extract the `.edn` file out of.

In Athens, click on the merge icon in the top bar.

![](/img/gitbook/import.png)

Click **Choose File**, then search for the `.edn` file on your system.

Athens tells you how many of the pages are [shared](#import) between your existing graph and the content you're importing from Roam.

Click **Merge** to finish.

### Merging shared pages

When importing pages that have the same title as an existing page in your Athens graph, the default merge strategy is to place the imported content at the bottom of the existing page.

Athens creates a block with the text: `[[Roam Import]] [[DATE]] [[FILE.edn]]`, then nests all the imported content in that block.

![](/img/gitbook/import_shared.png)

This also creates pages for **Roam Import**, the date of the merge \(if the [daily note](#daily-notes) doesn't already exist\), and the name of the imported file. Each of these can be useful to explore how your Roam graph was imported into Athens.

## Pages

### Bidirectional Links

Athens uses **bidirectional links** to help you organize your knowledge graph.

Bidirectional links are a little different from the normal one-way links \(aka "[monolinks](https://maggieappleton.com/bidirectionals)"\) you're used to seeing on the web. Normal links point from A to B, which is great for connecting information or leading readers down a particular path, but they don't help anyone who wants to explore _from B back to A_.

When you create a bidirectional link in Athens, you're creating two pages that are aware of each other. A links to B through what _looks_ like a one-way link, but then B points back to A via a list of references.

Create bidirectional links

To create a link, type `[[` in the outliner. A dropdown appears to help you search for an existing page that you want to link to from the current page. 

Move between the items in the dropdown with the up and down arrow keys, then hit `Enter` to select one, or click on the page you're looking for.

If you want to link to a page that doesn't yet exist, finish typing the title you'd like that page to have, then hit `Enter` or `]]` to finish creating the link.

Once you move to a different block, the link syntax turns into an active bidirectional link.

{% hint style="info" %}
Links also work with either`#`, or `#[[]]` syntax, such as `#Website` or `#[[Website]].` These links function the same, but the outliner renders them in the default text color, and they use a `#` symbol instead of `[[Website]]` symbols.
{% endhint %}

### Linked References

As mentioned above, the links you create between pages are bidirectional, which means they appear on both "sides" of the link.

On the page being linked to, these links appear in the **Linked References** section below the outliner.

![](/img/gitbook/links_linked-references.png)

In this example, clicking on the **May 10, 2021** or **Website redesign** links take you directly to those pages.

### Unlinked References

Athens gathers **Unlinked References** any time a page has text that matches the title of a page you already created but isn't already linked.

For example, here's an unlinked reference to the **Zlatica** page from another page.

![](/img/gitbook/links_unlinked-references.png)

You can leave this unlinked, or you can click the **Link** button to automatically wrap the string in Athens' link syntax and create a new bidirectional link.

Now that you understand bidirectional links, time to take a look at Athens' other primary way of connecting pages, blocks, and ideas together: [block references](#block-references).

## Blocks

### Block References

Block references embed the content of a single block into your current page. 

Like [bidirectional links](#bidirectional-links), block references create connections between two pages in your Athens knowledge graph. Once you create a block reference, you can navigate between the two pages using the [Linked References](#bidirectional-links) on either page.

Create a block reference

To create a block reference, type `((` into the outliner. A dropdown appears to help you search for an existing block you want to reference on your current page.

Move between the items in the dropdown with the up and down arrow keys, then hit `Enter` to select one, or click on the block you're looking for.

Once you move to a different block, the `(())` syntax turns into a block reference, which gets an orange underline to differentiate it from other blocks on your page.

![](/img/gitbook/blocks_embed.png)

Navigate to a block's parent page

If you click on a block reference, Athens takes you to the zoomed-in view of the block in question.

![](/img/gitbook/block-reference_zoom.png)

Click the title above the block to navigate to that page, or use Linked References to jump to related pages in your knowledge graph.

View pages that reference a particular block

Every time you reference a block, Athens puts a counter to its right to indicate how many times you referenced it in other pages in your knowledge graph.

Click on this counter to view all these links in the right sidebar.

![](/img/gitbook/block-reference_links.png)

### Block Embed

Similar to [block references](#block-references), block embeds allow you to embed blocks into your current page. Each block embed can display the contents of a single block, and its children. The major differences from a block reference is that in a block embed, you can zoom into a bullet, view the children of a bullet and make edits to the original block.

Unlike [bidirectional links](#bidirectional-links), block embeds do not create connections between two pages in the Athens knowledge graph.

Create a block embed

To create a block embed, hit the ~/~ key to open the slash menu and either filter the results by continuing to type or scroll till you find the block embed.

![](/img/gitbook/block-embed-create.png) 

Hit `Enter` or click to create an embed. A dropdown appears to help you search for an existing block you want to reference on your current page.

Move between the items in the dropdown with the up and down arrow keys, then hit `Enter` to select one, or click on the block you're looking for. 

![](/img/gitbook/block-embed-dropdown.png) 

When you click out of the block, you will see a block that is now embedded.

 ![](/img/gitbook/block-embed-success.png) 

You can edit, zoom into a bullet, add links and create new bullets as well in the embed.

Edit the content in a block embed

Click any text in the inside of an embed. Type as you would in a regular block, the changes will be reflected across the original block itself and all the embeds leading to it.

Edit the block embed itself

Click the pen icon in the top-right corner to change the source of a block embed.

## Daily Notes

To access your daily notes from anywhere in your graph, click on the calendar icon in the top panel or type `Alt/Option` + `d`. In this mode, Athens displays all your daily notes in a list that loads previous daily notes as you scroll down. As you reach the end of one note, the previous one loads.

Any individual daily note is also accessible via search. Click the **Find or Create a Page** button or type `Ctrl/⌘` + `k`.

## DB Picker

With Athens, each graph is its own database and because they are local, you can have as many databases as you want. In Athens, your database is stored on a file called “index.transit”. You can create, open and move databases from right within Athens. To access the database options, click the following icon on the toolbar.

![Image](https://user-images.githubusercontent.com/80150109/118108910-2f350100-b3fe-11eb-8601-8a0c2f3aaf92.png)

After clicking it, a popover will come up with three panes.

![Athens Database](https://user-images.githubusercontent.com/80150109/118109143-6dcabb80-b3fe-11eb-9064-330b0d532372.png)

### Creating a database

To create a database, in the pane that comes up, click the `New` button and specify a name for the database. Once you do this, click the `browse` button and navigate to where you want your database to be located. Hit `enter` and watch as your new database is created and launched.

**Tip: You can back up your database to the cloud by setting the location of the database to your dropbox folder!**

### Opening an existing database

On the “Open” pane of the database popup, click the `Open` button and navigate to the location of the index.transit file you want to load into Athens.

### Moving a database

On the “Open” pane of the database popup, click the `Move` button and navigate to the new location you would like your database to be located in.

## Keyboard Shortcuts

### Navigation

| Windows / Linux | macOS | Action |
| :--- | :--- | :--- |
| `Ctrl` + `k` | `⌘` + `k` | Search for or create a new page |
| `Alt` + `d` | `Option` + `d` | Jump to the [daily note](#daily-notes) |
| `Ctrl` + `\` | `⌘` + `\` | Open shortcuts sidebar |
| `Ctrl` + `Shift` + `\` | `⌘` + `Shift` + `\` | Open right sidebar |
| `Alt` + `←` | `Option` + `←` | Back |
| `Alt` + `→` | `Option` + `→` | Forward |

### Outliner and blocks

| Windows / Linux | macOS | Action |
| :--- | :--- | :--- |
| `/` | `/` | Open the slash command menu \(TODOs, embeds, dates\) |
| `Tab` | `Tab` | Indent block |
| `Shift` + `Tab` | `Shift` + `Tab` | Un-indent block |
| `Shift` + `Up` or `Down` | `Shift` + `Up` or `Down` | Select multiple blocks |
| `Ctrl` + `a` | `⌘` + `a` | Select all blocks on the page |
| `Ctrl` + `Enter` | `⌘` + `Enter` | Create a new TODO or mark an existing TODO as done |

### Text formatting

| Windows / Linux  | macOS | Action |
| :--- | :--- | :--- |
| `Ctrl` + `b` | `⌘` + `b` | Bold |
| `Ctrl` + `i` | `⌘` + `i` | Italic |
| `Ctrl` + `h` | `⌘` + `h` | Highlight |
| `Ctrl` + `y` | `⌘` + `y` | Strikethrough |

### Advanced

| Windows / Linux | macOS | Action |
| :--- | :--- | :--- |
| `Ctrl` + `g` | `⌘` + `g` | Open developer tools |

## Slash Commands

Slash commands are quick way to access powerful features within the Athens app. With slash commands, you can quickly create and insert embeds, block references, todos, page links, and even the current time.

To access the slash commands, type a `/` to bring up the menu and continue typing to filter through the commands or scroll through them using a keyboard or mouse.

![Walkthrough](https://user-images.githubusercontent.com/80150109/122540545-607c9e80-d046-11eb-84c3-dfbd32a7db53.gif)

### Current Slash Commands

| Command | Function |
| :--- | :--- |
| Add Todo | Inserts a "TODO" item into the current block |
| Current Time | Inserts the current time in 12 hour notation |
| Today | Inserts a link to today's daily note |
| Tomorrow | Inserts a link to tomorrow's daily note |
| Yesterday | Inserts a link to yesterday's daily note |
| YouTube Embed | Allows you to enter a link and embed a youtube video |
| iframe Embed | Allows you to enter a link and embed an iframe\(PDFs, Videos, Maps and more!\) |
| Block Embed | Creates a [Block Embed](#block-embed) |


## Graph Visualization

You've started taking notes, you've started linking ideas, what's next? Time to see your knowledge in action! The graph view is a bird’s eye view of your database, a way to identify connections and patterns in your graph. As you continue to take notes, you will start noticing clusters forming which, in addition to its functional purpose, is a way to marvel at your growing database.

![A sample graph view](https://user-images.githubusercontent.com/80150109/120890130-7b025100-c61e-11eb-8ead-4e9a8462b8fa.png)

To access the global graph view, click on the icon in the toolbar or use the global command, `alt/option-g`.

![Click the &quot;bubble&quot; icon in the toolbar](https://user-images.githubusercontent.com/80150109/120890171-979e8900-c61e-11eb-89b5-6f284299ef0f.png)

### View customization in the graph view

You can customize the graph's forces and choose to filter out the daily notes and orphan nodes. The forces of the graph can be manipulated by changing the link distance and the attraction force of the nodes in the graph under the forces menu in the right corner of the graph view. Under the nodes menu, you can choose to hide daily notes and/or orphan nodes and also change the number of links that are highlighted upon hovering of the individual nodes.

### The local graph

The local graph is one of the most powerful aspects of the graph view in Athens and allows you to get a catch all view of the pages that are linked to the current page. It can even let you go a step further by showing you pages that are linked to the linked pages. It's excellent to identify similar topics and pages which you might not have considered as relevant.

To open the local graph, click the three dots next to the title of the page to reveal a dropdown menu. In the dropdown menu, click the **Show Local Graph** button.

![Open a local graph](https://user-images.githubusercontent.com/80150109/120890114-6d4ccb80-c61e-11eb-96ce-4a145423420d.png)

### Customizing the local graph

Similar to the global graph, you can customize the forces of the graph, but there is something that is local specific, the "local depth" option. This option is powerful because it not only allows you to find topics that you have directly linked in the page but also shows you the pages _linked_ to the pages you have directly linked.

![Example Use Case](https://user-images.githubusercontent.com/80150109/120890204-bbfa6580-c61e-11eb-89f6-dc9977903ff3.png)

In this image, you can also see notes that could be relevant to the food chain that you may not have explicitly thought about or linked to in the food chain page.

