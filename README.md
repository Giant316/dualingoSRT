# Create SRT with two languages 

Although the Google Chrome extension:  `Language Learning with Netflix` has done a great job in showing multiple subtitles on Netflix however it only works if the movies on Netflix come with multi-language subtitles. For most of the German movies on Netflix unfortunately only have German substitle so I can view the movie with the two languages I want (German and English) with this tool. [Substital](https://chrome.google.com/webstore/detail/substital-add-subtitles-t/kkkbiiikppgjdiebcabomlbidfodipjg?hl=en) is a Chrome extensions that allows us to load our own SRT file and play the subtitles on video online. So this is an alternative solution to watch Netflix with dual language by loading a customized SRT and this script is written to done so by converting the substitle downloaded from Netflix (saved as `.xml`) to a `.srt` file loaded with the default language and english. 

### Workflow of this script

+ convert XML file to SRT - taken from the work of [isaacbernat](https://github.com/isaacbernat/netflix-to-srt) 
+ translating the converted SRT to english - automatically managed through https://translate-subtitles.com using selenium package 
+ merging the two SRTs (converted SRT in step 1 and downloaded SRT in step 2) using srtmerge package

### Prerequisite

+ packages: selenium, srtmerge and shutil 
+ a downloaded substitle from Netflix (saved in xml)
+ safari browser with `Allow Remote Automation` setup / other browser (you have to edit the code, see `Setup Safari browser` section)

### How to download subtitle from Netflix

1. make sure the substitle option is off, if it’s not turn it off and the reload the video 
2. pause the video
3. navigate to network tab by opening developer tools (CMD+OPT+I - safari) or (CTRL+Shift+I - window)
4. clear all output 
5. input `?o=` as filter
6. load the subtitle then you will see a file appears in the network tab as following:
7. save the file as `.xml`

![nfx-sub](../main/nfx-sub.png?raw=true)

### Setup Safari browser to allow remote automation

1. Go to Safari -> Preferences and then tick `Show Develop menu in menu bar` 
2. Go to the `Develop` tab that appeared and click `Allow Remote Automation`

If you are using other browser, you have to install its web driver, for details, refer [here](https://www.pluralsight.com/guides/web-scraping-with-selenium). Once the remote automation has been setup, then we can automatically upload and download the SRT for translaiton on https://translate-subtitles.com through selenium package. Change the code as following if you are using other browser: 

+ change the line`browser = webdriver.Safari()`  to `browser = webdriver.Firefox() or ` `browser = webdriver.Chrome()` 

### Run the Script

Since the translation website will download the file automatically to your default downlod folder, you have to specify it while running the script and you also need to provide the absolute path of the directory of your XML files as the input directory. The output directory is option, if it is not specified, the output SRT will be saved under the input directory. 

NOTE: the script will delete all the input XML files and SRT created in transition. It will only keep the SRT with dual language in your output directory (the input directory if not specified)

+ nagivate to the directory where the to_srt.py is in your console and run: `python to_srt.py -d /your/browser/download/directory -i /script/directory/` 

Load the generated SRT to [Substital](https://chrome.google.com/webstore/detail/substital-add-subtitles-t/kkkbiiikppgjdiebcabomlbidfodipjg?hl=en) and enjoy!

![100Dinge](../main/100Dinge.png?raw=true)

![DerGeilsteTag](../main/DerGeilsteTag.png?raw=true)



### Future Works

+ include other language supported in the translation website 

+ Experiment the translation with a trained Neural Machine Translation model 

  