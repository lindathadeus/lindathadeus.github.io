---
title: "Debugging Keyboard events in Sony Laptop"
date: 2024-10-06
layout: post
categories: [linux]
tags: [work, world, sony, general]
giscus_comments: true
authors:
  - name: Linda Joe Thadeus
    url: "https://lindathadeus.github.io"
    affiliations:
      - name: Org
      - name: Clg
  - name: ChatGPT
    url: "https://openai.com"
    affiliations:
      - name: OpenAI
---

### Diagnosing and Checking Key Events in My Old Sony Laptop

It wasn’t even a day—actually just a few hours—after I finally gave a purpose to my old Sony Laptop and updated its kernel for daily use when I noticed that the up arrow key wasn’t working.

At first, I thought I’d wasted all that time on a machine that I should probably just condemn. But there was something more at play—this wasn't just any laptop. It was a gift from my mom, my pink laptop with my name engraved on it. The emotional value was enough to keep me going. I couldn’t give up on it that easily!

#### Debugging the Problem

Since I’d spent so much time already, I figured I’d start debugging. I created an event notifier for keyboard events using the following kernel module:

{% highlight c %}
static int notifier(struct notifier_block *nblock, unsigned long code, void *_param) {
    struct keyboard_notifier_param *param = _param;

    if (code == KBD_KEYCODE) {
        printk(KERN_INFO "Key press: scancode = %d\n", param->value);
    }

    return NOTIFY_OK;
}

static struct notifier_block nb = {
    .notifier_call = notifier
};
{% endhighlight %}

The idea was to capture and log any key events. Pressing the up arrow...nothing. Sigh.

#### Physical Troubleshooting

I tried something else. I removed the key, dusted it off, cleaned everything, and reattached it. Still no events. Another sigh.

Then, in what felt like a desperate attempt, I removed the key once again. At this point, I was sure I’d broken something—both the key and my heart. But before giving up completely, I tried pressing the actual rubber underneath the key that triggers the event.

Success! Events were detected, but only when pressing the rubber directly—not with the key attached.

#### The Final (Temporary) Fix

With a bit of cello tape (yes, you read that right), I reattached the key to the keyboard. It’s not perfect, but it works—kind of. In the end, I’m using SSH to access my Sony laptop, but at least I know the up key is functional. And even if I don’t use it, just knowing it’s working gives me a sense of relief.

---

**What do you think?** Let me know your thoughts in the comments below.
