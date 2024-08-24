---
title: "My bashrc"
date: 2024-08-24
layout: post
categories: linux
tags: 
giscus_comments: true
featured: true
authors:
- name: Linda Joe Thadeus
url: "https://lindathadeus.github.io"
affiliations:
name: SuSE, NITK
---

# My bashrc

{% highlight python %}
# some more ls aliases
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias vi='vim'

# Alias definitions.

alias date1='date +"%d%B-%T"'
alias date0='date1|cut -d':' -f1'
alias gitlsco='git status -s'
alias gitco='git checkout'

patchfile() {
  git diff $1 > ~/patc
  patch $1 < ~/patc
}

newmd() {
	cd /lindathadeus.github.io/_posts
  if [ -z "$1" ]; then
    FILENAME=$(date +"%Y-%m-%d")-new-post.md
  else
    FILENAME=$(date +"%Y-%m-%d")-$1.md
  fi
  touch $FILENAME
  echo "---" > $FILENAME
  echo "title: \"${2:-New Post}\"" >> $FILENAME
  echo "date: $(date +"%Y-%m-%d %H:%M:%S")" >> $FILENAME
	echo "layout: post" >> $FILENAME
	echo "categories: $3" >> $FILENAME
	echo "tags: " >> $FILENAME
	echo "giscus_comments: true" >> $FILENAME
	echo "featured: true" >> $FILENAME
	echo "authors:" >> $FILENAME
  echo "- name: Linda Joe Thadeus" >> $FILENAME
    echo "url: \"https://lindathadeus.github.io\"" >> $FILENAME
    echo "affiliations:" >> $FILENAME

  echo "---" >> $FILENAME
  echo "" >> $FILENAME
  echo "# $2" >> $FILENAME
  echo "" >> $FILENAME
  echo "Your content here." >> $FILENAME
	echo "---" >> $FILENAME
	echo "**What do you think?** Let me know your thoughts in the comments below." >> $FILENAME
	echo "$FILENAME created."
}

nurture() {
	mkdir -p /tasks/nurture/$1/{1-seed,1-soil,2-sowing,3-nourishing,4-fencing,4-pruning,5-harvesting}
	cd /tasks/nurture/$1
}

echo "
  ________                     .___        .___
 /  _____/   ____    ____    __| _/      __| _/_____   ___.__.
/   \  ___  /  _ \  /  _ \  / __ |      / __ | \__  \ <   |  |
\    \_\  \(  <_> )(  <_> )/ /_/ |     / /_/ |  / __ \_\___  |
 \______  / \____/  \____/ \____ |     \____ | (____  // ____|
        \/                      \/          \/      \/ \/
"

echo ""
echo "Today is a good day :)"
{% endhighlight %}

---
**What do you think?** Let me know your thoughts in the comments below.
