# Supervisor_Yocto

Sources : 
- https://git.tansorier.fr/micka/presentations/raw/branch/master/Yocto-RapsberryPi-devtool-Ansible.pdf
- https://wiki.yoctoproject.org/wiki/images/archive/0/0d/20200702141904%21DD5_Security_Hardening_NA20.pdf
- https://www.linuxtricks.fr/wiki/rhel-et-derivees-fedora-administrer-sa-machine-avec-cockpit

git clone git://git.yoctoproject.org/poky -b rockoc
cd poky
git clone git://git.yoctoproject.org/meta-raspberrypi -b rocko
git clone git://git.openembedded.org/meta-openembedded -b rocko
. oe-init-build-env

Paramétrer le local.conf (MACHINE / DISTRO)

$POKY/build/conf/local.conf

MACHINE ="raspberrypi3-64"

$POKY/build/conf/bblayers.conf

Rajouter la layers
BBLAYERS +=" \${TOPDIR}/../meta-raspberrypi \
${TOPDIR}/../meta-openembedded/meta-python \
${TOPDIR}/../meta-openembedded/meta-oe \"

Compilation
bitbake core-image-minimal

Ajouter son layer custom
mkdir -p meta-meetup/conf

conf/layer.conf

BBPATH .=":${LAYERDIR}"
# We have recipes-* directories, add to BBFILESBBFILES 
+="${LAYERDIR}/recipes-*/*/*.bb \
${LAYERDIR}/recipes-*/*/*.bbappend"

BBFILE_COLLECTIONS +="meetup"
BBFILE_PATTERN_meetup ="^${LAYERDIR}/"
BBFILE_PRIORITY_meetup ="10"
