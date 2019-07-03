# conda

## default

conda info
conda update -n base conda
conda update anaconda

## workspace

conda create --name ENVNAME python=3.7
conda activate ENVNAME
conda activate /path/to/environment-dir

conda env list

conda deactivate

conda list
conda list --name ENVNAME
conda list --revisions
conda list --name ENVNAME --revisions
conda install --name ENVNAME --revision REV_NUMBER
conda remove --name ENVNAME --all

## sharing environment

conda create --clone ENVNAME --name NEWENV
conda env export --name ENVNAME > envname.yml
conda env create --file envname.yml
conda env create
conda list --explicit > pkgs.txt
conda create --name NEWENV --file pkgs.txt

## install

conda search PKGNAME=3.1 "PKGNAME[version='>=3.1.0,<3.2']"
anaconda search FUZZYNAME
conda install conda-forge::PKGNAME
conda install PKGNAME==3.1.4
conda install "PKGNAME[version='3.1.2|3.1.4']"
conda install "PKGNAME>2.5,<3.2"
conda config --all channels CHANNELNAME

## etc

conda search PKGNAME --info
conda clean --all
conda uninstall PKGNAME --name ENVNAME
conda update --all --name ENVNAME
conda install --yes PKG1 PKG2
conda config --show
conda config --show-sources
