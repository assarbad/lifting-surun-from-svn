all: surun.fi

surun.fi: surun.lift svnrepo
	reposurgeon "script $<"

clean:
	rm -rf surun-git
	rm -f surun.fi

rebuild: clean all

.PHONY: all rebuild clean
.NOTPARALLEL: all rebuild clean
