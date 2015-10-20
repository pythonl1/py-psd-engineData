py-psd-engineData
=================

Reads the text, font type, font size and color from a photoshop psd file

To first obtain the engineData you will need to install psd-tools, then you can parse the engineData with the following:

#HOW TO

    from psd_tools import PSDImage
    from engineData import getFontAndColorDict
    #open the psd
    fname = 'myPsdName.psd'
    psd = PSDImage.load(fname)


    for layer in reversed(psd.layers):
        #get the raw engine data
        rawData = layer.tagged_blocks.TYPE_TOOL_OBJECT_SETTING.text_data.items
        rawDataTuple = [tup[1] for tup in rawData]
        rawDataTuple.reverse()
        rawDataValue = rawDataTuple[0].value
        
        propDict= {'FontSet':'','Text':'','FontSize':'','A':'','R':'','G':'','B':''}
        getFontAndColorDict(propDict,rawDataValue)
        #Then just index into the dictionary to get the values
        myText = propDict['Text']
        myFont = propDict['FontSet']
  
  
  *note A R G B are percentages so to get the actual value multiply by 255
