# tu-design-setup
How to set up the LaTeX design of TU Darmstadt on Ubuntu or other related Linux distros:

## 0. Requirements
You first need a LaTeX distribution installed on your system. I recommend `TeXLive`: 
Open a terminal and run 
```
sudo apt install texlive texlive-lang-german texlive-extra-fonts
``` 
to install TeXLive and extra fonts for math symbols.

## 1. Download fonts
First, download the TU fonts from [here](https://www.intern.tu-darmstadt.de/arbeitsmittel/dokumente_formulare/details_5_106048.de.jsp). Extract the archive and install all fonts in the `darmstadt/ttf` folder.
Next, we need the font mappings for LaTeX: Go to the [FKP lab page](http://exp1.fkp.physik.tu-darmstadt.de/tuddesign/) and download `tudfonts.zip`. 

## 2. Download latex tudesign package
Go to the [TU corporate design page](https://www.intern.tu-darmstadt.de/arbeitsmittel/corporate_design_vorlagen/index.de.jsp). Open the `LaTeX: Große Berichte, Dissertationen – Vorlagen (+)` dropdown and download `Paket tudesign` and `Paket tudesign-thesis`.

## 3. Merge all packages
First, create a new folder called `tudesign-tmp` in your downloads folder. We want to merge all packages into the `tudesign-tmp` folder such that their folder structures line up. 

Start by extracting `latex-tudesign_*.zip` into the folder we just created. Next, extract `latex-tudesign-thesis_*.zip` such that the `texmf` folder is merged with the existing one from the previous package.
Finally, extract `tudfonts-tex_*.zip` and make sure that the `texmf` folder is merged again.

## 4. Move texmf
Now, we need to move the texmf folder to the correct location so it can be found by LaTeX.
Open a terminal in the `tudesign-tmp` folder. 
Run the following command to copy the texmf folder to the correct location:
```
sudo cp -r texmf/* /var/lib/texmf/
```
This is installing the design system-wide. That is why `sudo` is needed.

## 5. Include fonts
Run the following commands to register the font mappings in LaTeX:
```
sudo texhash
sudo updmap -sys --enable Map 5ch.map
sudo updmap -sys --enable Map 5fp.map
sudo updmap -sys --enable Map 5sf.map
```
To check if everything worked correctly, you can run this command:
```
updmap -sys --listmaps | egrep "^Map[[:blank:]]*5"
```
You should see the following response:
```
Map	5ch.map	enabled	/etc/texmf/web2c/updmap.cfg
Map	5fp.map	enabled	/etc/texmf/web2c/updmap.cfg
Map	5sf.map	enabled	/etc/texmf/web2c/updmap.cfg
```

## 6. Profit
Congratulations! You should now be able to compile `.tex` files with the tudesign and tu fonts.

Special thanks to Clemens v. Loewenich, Johannes Werner und Jannik Vieten for their tutorial on the FKP page. 
This guide is based on their work with some adjustments where necessary. 
