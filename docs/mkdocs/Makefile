.PHONY: docs-build docs-serve clean

DOCS_ROOT ?= $(shell cd "$(dirname '.')" && pwd -P)
DOCS_PORT ?= 9876

YML ?= $(wildcard *.yml)
LOCAL = $(YML:.yml=.local)

clean:
	@rm -rf $(DOCS_ROOT)/site $(DOCS_ROOT)/docs $(LOCAL)

docs-build: $(LOCAL)

mkdocs.local: mkdocs.yml
	@echo "setting up in $(DOCS_ROOT)"
	@cp $< $@
	@cp $(DOCS_ROOT)/index.md $(DOCS_ROOT)/docs/index.md
	@if [ -f $(DOCS_ROOT)/theme/global.yml ]; then cat $(DOCS_ROOT)/theme/global.yml >> $@ ; fi
	@$(echo -e "\ntheme: null\ntheme_dir: '$(DOCS_ROOT)/theme'\ndocs_dir: '$(DOCS_ROOT)/docs'\n" >> $@)
	@echo "building $*"
	@mkdocs build -f $@ --clean -q --site-dir "$(DOCS_ROOT)/site/$<"

docs-serve: $(LOCAL)
	@mkdocs serve --dev-addr=0.0.0.0:$(DOCS_PORT) -f $(DOCS_ROOT)/$(LOCAL)
