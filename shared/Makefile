DIRS = gimxcontroller gimxupdater gimxconfigupdater gimxlog gimxhid gimxinput gimxpoll gimxprio gimxserial gimxtimer gimxusb gimxgpp gimxconfigeditor

ifneq ($(OS),Windows_NT)
UHID=1
endif

ifeq ($(UHID),1)
DIRS := gimxuhid $(DIRS)
endif

BUILDDIRS = $(DIRS:%=build-%)
INSTALLDIRS = $(DIRS:%=install-%)
CLEANDIRS = $(DIRS:%=clean-%)
UNINSTALLDIRS = $(DIRS:%=uninstall-%)

all: $(BUILDDIRS)
$(DIRS): $(BUILDDIRS)
$(BUILDDIRS):
	$(MAKE) -C $(@:build-%=%) UHID=$(UHID)

build-gimxhid: build-gimxlog
build-gimxpoll: build-gimxlog
build-gimxprio: build-gimxlog
build-gimxserial: build-gimxlog
build-gimxtimer: build-gimxlog
build-gimxuhid: build-gimxlog

build-gimxconfigeditor: build-gimxcontroller
build-gimxconfigeditor: build-gimxhid build-gimxinput build-gimxtimer build-gimxpoll
build-gimxgpp: build-gimxhid
ifeq ($(UHID),1)
build-input: build-gimxuhid
endif
build-gimxinput: build-gimxhid build-gimxpoll
ifeq ($(OS),Windows_NT)
build-gimxusb: build-gimxtimer
endif

clean: $(CLEANDIRS)
$(CLEANDIRS): 
	$(MAKE) -C $(@:clean-%=%) clean

install: $(INSTALLDIRS) all
$(INSTALLDIRS):
	$(MAKE) -C $(@:install-%=%) install

uninstall: $(UNINSTALLDIRS)
$(UNINSTALLDIRS):
	$(MAKE) -C $(@:uninstall-%=%) uninstall

.PHONY: subdirs $(DIRS)
.PHONY: subdirs $(BUILDDIRS)
.PHONY: subdirs $(CLEANDIRS)
.PHONY: all clean
