LANG_ID = de
EXTRA_DIST = \
	sipxpbx \
	stdprompts_$(LANG_ID) \
	sipxecs-lang-$(LANG_ID).spec

promptsdir = $(datadir)/www/doc/stdprompts_$(LANG_ID)
prompts_SOURCE = \
	$(shell find $(srcdir)/stdprompts_$(LANG_ID) -name '*.wav' -type f -printf '%P\n')

confdir = @SIPX_JAVADIR@/sipXconfig
conf_DATA = sipxconfig-de.jar

conf_SOURCE = \
	$(shell find $(srcdir)/sipxpbx -name '*_$(LANG_ID).properties' -type f -printf '%P\n')

sipxconfig-de.jar :
	jar -cf $@ -C $(srcdir)/sipxpbx .

install-data-hook :
	$(info installing prompts)
	@echo "$$Installer" | \
	  InstallFileList="$(prompts_SOURCE)" \
	  InstallSourceDir=$(srcdir)/stdprompts_$(LANG_ID) \
	  InstallDestDir=$(DESTDIR)$(promptsdir) \
	  bash

x :
	$(info installing web ui)
	@echo "$$Installer" | \
	  InstallFileList="$(conf_SOURCE)" \
	  InstallSourceDir=$(srcdir)/sipxpbx \
	  InstallDestDir=$(DESTDIR)$(confdir) \
	  bash

# work around INSTALL limitations
# 1.  create directories before installing file 
# 2.  install path1/file into path2/path1/file, not path2/file
define Installer
	for f in $${InstallFileList}; do
	  ThisInstallDir=`dirname $${InstallDestDir}/$$f`
	  $(INSTALL) -d $${ThisInstallDir}
	  $(INSTALL) -t $${ThisInstallDir} $${InstallSourceDir}/$$f
	done;
endef
export Installer