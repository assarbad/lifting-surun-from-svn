PWD:=$(shell pwd)
NAME:=surun
SVNURL:=https://svn.code.sf.net/p/$(NAME)/code/
all: $(NAME).fi

$(NAME).fi: $(NAME).lift $(NAME).svn
	svnsync synchronize file:///$(PWD)/$(filter %.svn,$^)/
	reposurgeon "script $<"

clean:
	rm -rf $(NAME)-git
	rm -f $(NAME).fi

$(NAME): $(NAME).svn

$(NAME).svn: $(NAME).svn/hooks/pre-revprop-change
	svnsync initialize file:///$(PWD)/$@/ $(SVNURL)

$(NAME).svn/hooks/pre-revprop-change: $(NAME).svn/format
	echo "#!/usr/bin/env bash" > $@
	echo "exit 0" >> $@
	chmod +x $@

$(NAME).svn/format:
	svnadmin create $(dir $@)

rebuild: clean all

.PHONY: all rebuild clean
.NOTPARALLEL: all rebuild clean $(NAME)
