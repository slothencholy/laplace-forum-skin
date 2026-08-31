Hello.

This is a GitHub repository dedicated to recreating the funny little Laplace forum promotional images as an ao3 workskin.
Unfortunately, two steps into this project, I realized I didn't feel like torturing myself with CSS, and hacked it
together with duct tape, staples, and a dream. If you, for whatever reason, want to edit this page tremendously, the
consequences of my terrible CSS skills will probably come back to haunt you. However, if you just want to copy
paste new little forum messages for the gay scientists to say, it should work well enough. Hopefully?

# Basic Instructions
Paste the contents of [the style sheet](style.css) into 'Dashboard' --> 'Skins' --> 'My Work Skins' --> 'Create Work Skin'. 
Then apply it to a fic with the option 'Select work skin' under 'Choose a language'.

Of course, to get the skin to work correctly, you also need to apply the correct formatting to your fic, in order
to display all the posts nicely.

# HTML Format

## Design details and Foundation

I got lazy and didn't insert the Laplace forum header as a CSS element, so it should be added to the very first line:
```
<p class="blank">
    <img src="https://raw.githubusercontent.com/slothencholy/laplace-forum-ao3/refs/heads/main/decorative/header.jpg" class="header">
</p>
```
The 'blank' class is there because ao3 formatting will automatically add a paragraph there and mess up the spacing.

From then on, everything that comes next should be encased in a 'background' div, and then afterwards the 'main' div:
```
<div class="background">
    <div class="main">
        <!-- All other content -->
    </div>
</div>
```
The 'background' div will apply the Laplace textured background to everything, and the 'main' div will split up the
sections and create our sidebar.

At the very end, that sidebar needs to be inserted:
```
        <div class="sidebar">
            <img src="https://raw.githubusercontent.com/slothencholy/laplace-forum-ao3/refs/heads/main/decorative/login.jpg" class="image">
            <img src="https://raw.githubusercontent.com/slothencholy/laplace-forum-ao3/refs/heads/main/decorative/hot-topics.png" class="image">
            <img src="https://raw.githubusercontent.com/slothencholy/laplace-forum-ao3/refs/heads/main/decorative/logo.png" class="image">
            <img src="https://raw.githubusercontent.com/slothencholy/laplace-forum-ao3/refs/heads/main/decorative/buttons.png" class="image">
            <img src="https://raw.githubusercontent.com/slothencholy/laplace-forum-ao3/refs/heads/main/decorative/smalltext.png" class="image footer">
        </div>
    <!-- These last two closing tags are for the 'main' and 'background' div -->
    </div>
</div>
```
This will add the fancy little icons on the side of the forum screen. The login button, the hot topics section, a 
logo, some funny looking buttons, and some official-looking text at the bottom of the screen. Speaking of, I got
too lazy to code that hot topics section, so it's entirely an image. If you want to make your own, you'll need to
bust out an image editing program. The [image file with layers](/decorative/hot-topics.psd) should help.

That's basically all the fluff. Once all this is done, the basic layout of the forum is completed, and we're
ready to add actual posts and threads.

## Main Forum Body

The forum is split into three basic elements: A title, a standalone post (with no direct replies), and a 
thread with 1+ replies. One standalone post will always be underneath the title. It's the 'main' post, 
but it looks visually identical to any other standalone post.

(For anyone new to HTML, any text that's not within the little carrots <> can be edited to display
whichever text you want. I have tried to help by adding nice placeholder text.)

Before the title is a little link to a forum directory, in which you can write whatever you want:
```
            <div class="breadcrumb">
                <div>Laplace &gt; Forum Branch Here</div>
            </div>
```

Then, the title post:
```
            <div class="card title post">
                <div>[General Topic] Actual Title</div>
            </div>
```
All three of those classes in the div are probably important.

After the title is the main post. Now, this is where things get a bit more complicated. The first 
element in each post is a 'user section', which differs based on if it's a standalone post or a
thread. Within that usersection, there are some other classes that indent the elements properly 
and measure out spacing.
After that, there is a body, and then an innerbody, which formats the text.
```
            <div class="post mainpost">
                <div class="usersection">
                    <div class="userindent firstcomment">
                        <img src="the-link-to-your-chosen-character.png" class="avatar">

                        <div class="userinfo">
                            <div class="tag">ID:MEANINGLESS-BUT-OFFICIAL-LOOKING-TEXT</div>
                            <div class="username">Forum Username</div>
                        </div>
                    </div>
                </div>
                <div class="body">
                    <div class="innerbody">
                        <div>
                            I'm a forum post created by the user above!
                        </div>
                    </div>
                </div>
            </div>
```
As stated previously, the 'main' post is visually the same as any standalone post. This same format
can be reused for any comment that doesn't have replies. As long as the block formatting stays 
intact, it can be slapped (almost) anywhere. Change the body text you can create any forum post
you want.


Now, there are threads. They're where things become hell. The entire comment chain is wrapped in a 
'thread' div, and 'posts' are placed within. Importantly, the first post within a thread uses the
class "firstthread", and the contained usersection uses the class "firstcomment".
```
            <div class="thread">
                <div class="post firstthread">

                    <div class="usersection">
                        <div class="userindent firstcomment">
                            <img src="the-link-to-your-chosen-character.png" class="avatar">
                            <div class="userinfo">
                                <div class="tag">ID:MEANINGLESS-BUT-OFFICIAL-LOOKING-TEXT</div>
                                <div class="username">Forum Username</div>
                            </div>
                        </div>
                    </div>

                    <div class="body">
                        <div class="innerbody">
                            <div>I'm an ordinary comment that other people commented under!</div>
                        </div>
                    </div>
                </div>
```

The next post after that must use the class "firstreply" and "reply". All posts afterwards use 
that 'reply' tag, and all usersections instead use the 'userreply' class.
```
                <div class="post firstreply reply">

                    <div class="userreply">
                        <div class="userindent">
                            <img src="the-link-to-your-chosen-character.png" class="avatar">
                            <div class="userinfo">
                                <div class="tag">ID:MEANINGLESS-BUT-OFFICIAL-LOOKING-TEXT</div>
                                <div class="username">Forum Username</div>
                            </div>
                        </div>
                    </div>

                    <div class="body">
                        <div class="innerbody">
                            <div>I decided to comment to reply to the above post, and thus made it a thread!</div>
                        </div>
                    </div>
                </div>
```

After that, posts use the 'bodyreply' class. As many 'bodyreply' posts can be added to a thread
as you want.
```
                <div class="post bodyreply reply">
                    <div class="userreply">
                        <div class="userindent">
                            <img src="the-link-to-your-chosen-character.png" class="avatar">
                            <div class="userinfo">
                                <div class="tag">ID:MEANINGLESS-BUT-OFFICIAL-LOOKING-TEXT</div>
                                <div class="username">Forum Username</div>
                            </div>
                        </div>
                    </div>

                    <div class="body">
                        <div class="innerbody">
                            <div>I commented and made the thread longer. My classes are identical to the comment below!</div>
                        </div>
                    </div>
                </div>


                <div class="post bodyreply reply">
                    <div class="userreply ">
                        <div class="userindent">
                            <img src="the-link-to-your-chosen-character.png" class="avatar">
                            <div class="userinfo">
                                <div class="tag">ID:MEANINGLESS-BUT-OFFICIAL-LOOKING-TEXT</div>
                                <div class="username">Forum Username</div>
                            </div>
                        </div>
                    </div>
                    <div class="body">
                        <div class="innerbody">
                            <div>You can duplicate my surrounding div block as many times as you want within the thread!</div>
                        </div>
                    </div>
                </div>
```

The last post in a thread, however, uses the 'lastreply' class as well as 'bodyreply'.
```
                <div class="post bodyreply lastreply">

                    <div class="userreply ">
                        <div class="userindent">
                            <img src="the-link-to-your-chosen-character.png" class="avatar">
                            <div class="userinfo">
                                <div class="tag">ID:MEANINGLESS-BUT-OFFICIAL-LOOKING-TEXT</div>
                                <div class="username">Forum Username</div>
                            </div>
                        </div>
                    </div>

                    <div class="body">
                        <div class="innerbody">
                            <div>I'm the last reply in the thread, and have slightly different formatting from the other replies.</div>
                        </div>
                    </div>
                </div>
            </div>
```
Just like with posts, a thread can be used as many times as you want.

In the event that a thread is only two posts, and the reply is both the first AND last reply, it should have the classes 'firstreply',
'reply' and 'lastreply'.

```
            <div class="thread">

                <div class="post firstthread">
                    <div class="usersection">
                        <div class="userindent firstcomment">
                            <img src="character.jpg" class="avatar">
                            <div class="userinfo">
                                <div class="tag">ID</div>
                                <div class="username">Username</div>
                            </div>
                        </div>
                        
                    </div>
                    <div class="body">
                        <div class="innerbody">
                            <div>I'm a thread with only one comment.</div>
                        </div>
                    </div>
                </div>

                <div class="post firstreply reply lastreply">
                    <div class="userreply ">
                        <div class="userindent">
                            <img src="character.jpg" class="avatar">

                            <div class="userinfo">
                                <div class="tag">ID</div>
                                <div class="username">Username</div>
                            </div>
                        </div>
                    </div>
                    <div class="body">
                        <div class="innerbody">
                            <div>I'm the last reply.</div>
                            
                        </div>
                    </div>
                </div>
            </div>
```

## Full Code Blocks

### First Post
Before the title is a little link to a forum directory, in which you can write whatever you want:
```
            <div class="breadcrumb">
                <div>Laplace &gt; ForumBranchHere</div>
            </div>
            <div class="card title post">
                <div>[GeneralTopic] ActualTitle</div>
            </div>
            <div class="post mainpost">
                <div class="usersection">
                    <div class="userindent firstcomment">
                        <img src="character.png" class="avatar">

                        <div class="userinfo">
                            <div class="tag">ID</div>
                            <div class="username">Username</div>
                        </div>
                    </div>
                </div>
                <div class="body">
                    <div class="innerbody">
                        <div>
                            POSTBODY
                        </div>
                    </div>
                </div>
            </div>
```

### Standalone Post
```
            <div class="post mainpost">
                <div class="usersection">
                    <div class="userindent firstcomment">
                        <img src="character.png" class="avatar">

                        <div class="userinfo">
                            <div class="tag">ID</div>
                            <div class="username">Username</div>
                        </div>
                    </div>
                </div>
                <div class="body">
                    <div class="innerbody">
                        <div>
                            POSTBODY
                        </div>
                    </div>
                </div>
            </div>
```

### Thread
```
            <div class="thread">
                <div class="post firstthread">

                    <div class="usersection">
                        <div class="userindent firstcomment">
                            <img src="character.png" class="avatar">
                            <div class="userinfo">
                                <div class="tag">ID</div>
                                <div class="username">Username</div>
                            </div>
                        </div>
                    </div>

                    <div class="body">
                        <div class="innerbody">
                            <div>THREADSTART</div>
                        </div>
                    </div>
                </div>


                <div class="post firstreply reply">

                    <div class="userreply">
                        <div class="userindent">
                            <img src="character.png" class="avatar">
                            <div class="userinfo">
                                <div class="tag">ID</div>
                                <div class="username">Username</div>
                            </div>
                        </div>
                    </div>

                    <div class="body">
                        <div class="innerbody">
                            <div>FIRSTREPLY</div>
                        </div>
                    </div>
                </div>


                <div class="post bodyreply reply">
                    <div class="userreply">
                        <div class="userindent">
                            <img src="character.png" class="avatar">
                            <div class="userinfo">
                                <div class="tag">ID</div>
                                <div class="username">Username</div>
                            </div>
                        </div>
                    </div>

                    <div class="body">
                        <div class="innerbody">
                            <div>BODYREPLY</div>
                        </div>
                    </div>
                </div>

                <div class="post bodyreply reply">
                    <div class="userreply">
                        <div class="userindent">
                            <img src="character.png" class="avatar">
                            <div class="userinfo">
                                <div class="tag">ID</div>
                                <div class="username">Username</div>
                            </div>
                        </div>
                    </div>
                    <div class="body">
                        <div class="innerbody">
                            <div>BLOCKREPLY</div>
                        </div>
                    </div>
                </div>

                <div class="post bodyreply lastreply">

                    <div class="userreply ">
                        <div class="userindent">
                            <img src="character.png" class="avatar">
                            <div class="userinfo">
                                <div class="tag">ID</div>
                                <div class="username">Username</div>
                            </div>
                        </div>
                    </div>

                    <div class="body">
                        <div class="innerbody">
                            <div>LASTREPLY</div>
                        </div>
                    </div>
                </div>
            </div>
```

## Other small details
- Missing a closing `</div>` block somewhere can really mess up the formatting, so be careful!
- The avatar file size is roughly 50px by 50px. Any image used as an avatar will be automatically resized.
- The spacing can get slightly misaligned if the Username is long enough to wrap. To solve this I just made the font size smaller. There is a more elegant solution somewhere.
- The css was created by cutting up images and using them as background elements...... I then decided to hardcode margins to space everything out properly.
- I hate css.
- I like writing a lot more. Go read [my fic!](https://archiveofourown.org/works/90083486)