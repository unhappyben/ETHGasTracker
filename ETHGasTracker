async function getGasOracleData() {
    try {
        //let apiKey = "REPLACEWITHYOURS";
        //&apikey=${apiKey}
        let gasOracleURL = `https://api.etherscan.io/api?module=gastracker&action=gasoracle`;
        let gasRequest = new Request(gasOracleURL);
        let gasResponse = await gasRequest.loadJSON();
        return gasResponse.result;
    } catch (error) {
        console.error("Error fetching gas oracle data:", error);
        return null;
    }
}

let gasData = await getGasOracleData();
if (gasData) {
    let safeGasPrice = gasData.SafeGasPrice;
    let fastGasPrice = gasData.FastGasPrice;

    let widget = createWidget(safeGasPrice, fastGasPrice);

    if (config.runsInWidget) {
        Script.setWidget(widget);
        Script.complete();
    } else {
        widget.presentSmall();
    }
} else {
    console.error("Gas oracle data is undefined.");
}

function createWidget(safeGasPrice, fastGasPrice) {
    let w = new ListWidget();
    
    let safeGasPriceText = w.addText(`Safe Gas Price: ${safeGasPrice} Gwei`);
    safeGasPriceText.textSize = 12;
    
    let fastGasPriceText = w.addText(`Fast Gas Price: ${fastGasPrice} Gwei`);
    fastGasPriceText.textSize = 12;
    
    return w;
}
