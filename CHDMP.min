// ==UserScript==
// @name         CryptoHopper Darkmode Plus
// @version      0.1
// @description  CSS overwrite for Tampermonkey to make Cryptohopper actually dark + it adds some of my favorite 3rd party features and fixes some layout issues
// @author       NE0NBLACK
// @twitter      @NblackNe0
// @Discord      NE0NBLACK#5876
// @donate       NE0NBLACK.ETH
// @match        https://www.cryptohopper.com/*
// @match        https://s.tradingview.com/*
// @icon         https://www.google.com/s2/favicons?domain=www.cryptohopper.com
// @grant        GM_addStyle
// @grant        GM.setClipboard
// @grant        GM_getValue
// @grant        GM_setValue
// ==/UserScript==

/* TradingView */
/* Inject script to change orderbook colors */
var orderbook_colors = document.createElement('script');
orderbook_colors.type = "text/javascript";
orderbook_colors.innerHTML = `
var orderbook_red_color = 'rgba(255, 0, 64, .25)'; // REDRGBA25 //
var orderbook_background = '#333'; // 80B //
var orderbook_green_color = 'rgba(0, 199, 87, .25)'; // GRNRGBA25 //
var orderbook_last_price = '#4D4D4D'; // 70B //
`;
document.getElementsByTagName('head')[0].appendChild(orderbook_colors);

/* Cryptohopper */
/* Inject script to change range slider colors (not working yet)*/
var setSliderColorsOverwrite = document.createElement('script');
var SliderColor_GRN = getComputedStyle(document.body).getPropertyValue('--SliderColor_GRN');
var SliderColor_RED = getComputedStyle(document.body).getPropertyValue('--SliderColor_RED');
var SliderColor_HB = getComputedStyle(document.body).getPropertyValue('--SliderColor_HB');
setSliderColorsOverwrite.type = "text/javascript";
setSliderColorsOverwrite.innerHTML = `
var color_strong_sell = "#FF0040", color_sell = "rgba(255, 0, 64, .50)", color_neutral = "#00B2C8", color_buy = "rgba(0, 199, 87, .50)", color_strong_buy = "#00C757";
script.type = "text/javascript";
(function setSliderColorsOverwrite(a, b) {
    var c = jQuery(a).parent("div"),
    d = c.find(".irs-single").eq(0),
    e = c.find(".irs-bar").eq(0);
    c = c.find(".irs-bar-edge").eq(0);
    "buy" == b ? (d.css("background", color_buy).css("color", "#FFF"), e.css("background-image", SliderColor_GRN), c.css("background-image", SliderColor_GRN) : "strong buy" == b ? (d.css("background", color_strong_buy).css("color", "#FFF"), e.css("background-image",
            SliderColor_GRN), c.css("background-image", SliderColor_GRN)) : "strong sell" == b ? (d.css("background", color_strong_sell).css("color", "#FFF"), e.css("background-image", SliderColor_RED), c.css("background-image", SliderColor_RED)) : "sell" == b ? (d.css("background", color_sell).css("color",
            "#FFF"), e.css("background-image", SliderColor_RED), c.css("background-image", SliderColor_RED)) : "neutral" == b && (d.css("background", color_neutral).css("color", "#FFF"), e.css("background-image", SliderColor_HB), c.css("background-image", SliderColor_HB))
})
(function sliderChangedOverwrite(a, b) {
    var c = "#sell_score_corrected";
    "#min_buy_score" == a && (c = "#buy_score_corrected");
    1 == jQuery(c + " option:selected").val() ? 85 <= b ? setSliderColorsOverwrite(a, "strong buy") : 65 <= b ? setSliderColorsOverwrite(a, "buy") : 35 < b ? setSliderColorsOverwrite(a, "neutral") : 35 >= b && 15 < b ? setSliderColorsOverwrite(a, "sell") : 15 >= b ? setSliderColorsOverwrite(a, "strong sell") : setSliderColorsOverwrite(a, "neutral") : .7 <= b ? setSliderColorsOverwrite(a, "strong buy") : .3 <= b ? setSliderColorsOverwrite(a, "buy") :  - .3 < b ? setSliderColorsOverwrite(a, "neutral") :  - .3 >= b &&  - .7 < b ? setSliderColorsOverwrite(a, "sell") :  - .07 >=
    b ? setSliderColorsOverwrite(a, "strong sell") : setSliderColorsOverwrite(a, "neutral")
})
`;
document.getElementsByTagName('head')[0].appendChild(setSliderColorsOverwrite);

/* Detailed stats forked from falcontx */
/* https://github.com/markrickert/cryptohopper-dashboard-watchlist */

try {
  // Only run this code on the intended page(s) (useful when @required in a parent script)
  if (["/dashboard"].includes(window.location.pathname))
    (function () {
      "use strict";
      var base = collect_currency;

      function statsDetail() {
        jQuery(
          "#statsinfo > div > div:nth-child(1) > div.col-xs-10 > p.text-muted.m-b-5.font-13.text-uppercase.pull-left"
        ).contents()[0].nodeValue = "Profit (gross + positions = current):  ";
        jQuery("#statsinfo > div > div:nth-child(1) > div.col-xs-10 > h4").prop(
          "id",
          "original"
        );
        jQuery("#original")
          .clone()
          .insertAfter("#original")
          .prop("id", "gross");
        jQuery("#original").hide();
        jQuery("#gross").clone().insertAfter("#gross").prop("id", "positions");
        jQuery("#positions")
          .clone()
          .insertAfter("#positions")
          .prop("id", "net");
        jQuery("#positions")
          .addClass("text-inverse")
          .css("border-bottom", "1px solid #555")
          .css("display", "inline-block");
        jQuery("#gross > strong > #stats_total_returns").prop(
          "id",
          "detail_total_gross"
        );
        jQuery("#positions > strong > #stats_total_returns").prop(
          "id",
          "detail_total_positions"
        );
        jQuery("#net > strong > #stats_total_returns").prop(
          "id",
          "detail_total_net"
        );
        jQuery("#gross > #stats_percent_change").prop(
          "id",
          "detail_percent_gross"
        );
        jQuery("#positions > #stats_percent_change").prop(
          "id",
          "detail_percent_positions"
        );
        jQuery("#net > #stats_percent_change").prop("id", "detail_percent_net");
        jQuery("#statsinfo > div > div:nth-child(3) > div.col-xs-10").prop(
          "id",
          "basetotal"
        );
        jQuery("#basetotal").append('<hr class="m-b-15">');
        jQuery("#basetotal").append(
          `<p class="text-muted m-b-5 font-13 text-uppercase">${base} available on exchange:</p><h4 class="m-t-0 m-b-5 counter text-inverse"><strong><span id="val_baseavail"></span></strong> <span id="val_baseavail_percent_change_wrapper" style="display: inline;">(<span id="val_baseavail_percent_change"></span>%)</span></h4>`
        );
        updateValues();
      }

      function updateValues() {
        //var netProfit = parseFloat(jQuery("#original > strong > #stats_total_returns").text());
        var positions = parseFloat(jQuery("#stats_total_positions").text());
        var startBalance = String(hopper_start_balance).replace(",", "");
        var totalBalance = String(current_hopper_balance).replace(",", "");
        var netProfit = totalBalance - startBalance;
        var grossProfit = netProfit - positions;
        var netProfitPct = (netProfit / startBalance) * 100;
        var positionsPct = (positions / startBalance) * 100;
        var grossProfitPct = (grossProfit / startBalance) * 100;
        var baseAvail = $(
          `#current_assets_table > tbody > tr > td:nth-child(1) > b`
        )
          .filter(function () {
            return $(this).text() == base;
          })
          .closest("tr")
          .children()
          .eq(1)
          .text();
        var baseAvailPct = (baseAvail / totalBalance) * 100;

        jQuery("#detail_total_gross").text(grossProfit.toFixed(2));
        jQuery("#detail_percent_gross").text(grossProfitPct.toFixed(2));
        jQuery("#detail_total_positions").text(positions.toFixed(2));
        jQuery("#detail_percent_positions").text(positionsPct.toFixed(2));
        jQuery("#detail_total_net").text(netProfit.toFixed(2));
        jQuery("#detail_percent_net").text(netProfitPct.toFixed(2));
        if (typeof jQuery("#val_totalbalance").attr("class") != "undefined") {
          jQuery("#net").attr(
            "class",
            "m-t-0 m-b-5 " + jQuery("#val_totalbalance").attr("class")
          );
        } else {
          jQuery("#net").attr(
            "class",
            jQuery("#val_totalbalance").parent().parent().attr("class")
          );
        }
        if (grossProfit >= 0) {
          jQuery("#gross").attr("class", "m-t-0 m-b-5 text-success");
        } else {
          jQuery("#gross").attr("class", "m-t-0 m-b-5 text-danger");
        }
        jQuery("#val_baseavail").text(baseAvail);
        jQuery("#val_baseavail_percent_change").text(baseAvailPct.toFixed(2));
      }

      function watchStatsData() {
        statsDetail();
        jQuery(document).ajaxComplete(updateValues);

        //$('body').on('DOMSubtreeModified', '#original', function() {
        // $('body').on('DOMSubtreeModified', '#val_totalbalance', function() {
        //   updateValues();
        // });
        // $('body').on('DOMSubtreeModified', '#stats_total_positions', function() {
        //   updateValues();
        // });
      }

      jQuery(() => {
        watchStatsData();
      });
    })();
} catch (err) {
  console.log(
    `Error in script target-restore.user.js: ${err.name}: ${err.message}`
  );
}

(function () {
  "use strict";

  function watchUpdates() {
    jQuery(document).ajaxComplete(updateValues);
  }

  jQuery(() => {});
})();

/* Disable hoppie forked from 0SkillAllLuck */
/* https://github.com/0SkillAllLuck/cryptohopper_scripts */

(function () {
  "use strict";

  jQuery(() => {
    GM_addStyle(`
      img.hoppie-paperclip,
      img.hoppiePaperclipAnimation,
      div.hoppie-speech-container,
      div._hj_feedback_container, /* disable feedback */
      div.fc-widget-small{ /* disable support chat */
        display: none !important;
      }
    `);
  });
})();


/* Backtest allowed coins forked from 0SkillAllLuck */
/* https://github.com/0SkillAllLuck/cryptohopper_scripts */

(function () {
    'use strict';


    function socketMessagesHandler(d) {
        d = JSON.parse(d);
        "chartdata" == d.type ? (result_chart_data_markings = [], drawResultChart(d, "nottest")) : "chartdatatest" == d.type ? (result_chart_data_markings = [], drawResultChart(d, "test")) : "progress" == d.type ? processProgressInfo(d, "test") : "trade" == d.type ? addTradeBacktest(d, "nottest") : "selectedtrades" == d.type ? addMultipleTradeBacktest(d, "nottest") : "selectedtradestest" == d.type ? addMultipleTradeBacktest(d, "test") : "tradetest" == d.type ? addTradeBacktest(d, "test") : "resettrades" == d.type ? (jQuery("#result_trades_table tbody tr").remove(),
    result_chart_data_markings = [],
    redrawChart("nottest")) : "resettradestest" == d.type ? (jQuery("#result_trades_table_test tbody tr").remove(),result_chart_data_markings = [],redrawChart("test")) : "result" == d.type ? outputBackTest(d.result) : "resulttest" == d.type ? outputConfigTest(d.result) : "error" == d.type && backtestErrorMessage(d.error)

        if (d.type == "result" || d.type == "resulttest") {
            const currentList = jQuery('#coinList').val().split(",");
            const currentIndex = parseInt(jQuery('#coinIndex').val());
            if (currentIndex < currentList.length) {
                jQuery('#coinIndex').val(currentIndex + 1);
                jQuery("#coin_test").val(currentList[currentIndex]).change();
                setTimeout(function(){ startBackTestConfig(); }, 2000);
            } else {
                swal({ title: 'Success', text: 'Backtest completed, all allowed coins were tested!', type: 'success' });
            }

        }
    }

    function doBacktestAllowedCoins() {
        var overrideScript = document.createElement('script');
        overrideScript.innerHTML = socketMessagesHandler.toString().replace(/([\s\S]*?return;){2}([\s\S]*)}/,'$2');
        document.body.appendChild(overrideScript);

        $.get('https://www.cryptohopper.com/config', function(configPage) {
            jQuery('#coinList').val($(configPage).find('#allowed_coins').val().join(','));
            jQuery('#coinIndex').val('1');

            jQuery("#coin_test").val(jQuery('#coinList').val().split(",")[0]).change();
            setTimeout(function(){ startBackTestConfig(); }, 250);
        });
    }

    function addElements() {
        const backtestAllowedCoinsCoinList = jQuery('<input id="coinList" hidden></input>');
        const backtestAllowedCoinsCoinIndex = jQuery('<input id="coinIndex" hidden></input>');
        const backtestAllowedCoinsButton = jQuery('<button type="button" class="btn btn-default" style="margin-top:15px">Backtest allowed Coins</button>');
        backtestAllowedCoinsButton.on('click', () => doBacktestAllowedCoins());
        jQuery('#backtest-config > div > div:nth-child(1) > div').append(backtestAllowedCoinsCoinList).append(backtestAllowedCoinsCoinIndex).append(backtestAllowedCoinsButton);
    }

    jQuery(document).ready(() => addElements());
})();

/* Backtest muliple settings forked from 0SkillAllLuck */
/* https://github.com/0SkillAllLuck/cryptohopper_scripts */

(function () {
    'use strict';


    function socketMessagesHandler(d) {
        d = JSON.parse(d);
        "chartdata" == d.type ? (result_chart_data_markings = [], drawResultChart(d, "nottest")) : "chartdatatest" == d.type ? (result_chart_data_markings = [], drawResultChart(d, "test")) : "progress" == d.type ? processProgressInfo(d, "test") : "trade" == d.type ? addTradeBacktest(d, "nottest") : "selectedtrades" == d.type ? addMultipleTradeBacktest(d, "nottest") : "selectedtradestest" == d.type ? addMultipleTradeBacktest(d, "test") : "tradetest" == d.type ? addTradeBacktest(d, "test") : "resettrades" == d.type ? (jQuery("#result_trades_table tbody tr").remove(),
    result_chart_data_markings = [],
    redrawChart("nottest")) : "resettradestest" == d.type ? (jQuery("#result_trades_table_test tbody tr").remove(),result_chart_data_markings = [],redrawChart("test")) : "result" == d.type ? outputBackTest(d.result) : "resulttest" == d.type ? outputConfigTest(d.result) : "error" == d.type && backtestErrorMessage(d.error)

        if (d.type == "result" || d.type == "resulttest") {
            var tpList = jQuery('#tpList').val().split(",").filter(tp => tp.trim().length > 0);
            var tpIndex = parseInt(jQuery('#tpIndex').val());
            var slList = jQuery('#slList').val().split(",").filter(sl => sl.trim().length > 0);
            var slIndex = parseInt(jQuery('#slIndex').val());
            var tslList = jQuery('#tslList').val().split(",").filter(tsl => tsl.trim().length > 0);
            var tslIndex = parseInt(jQuery('#tslIndex').val());

            tpIndex += 1;
            if (tpIndex < tpList.length) {
                jQuery('#tpIndex').val(tpIndex);
            } else {
                tpIndex = 0;
                jQuery('#tpIndex').val(tpIndex);

                slIndex += 1;
                if (slIndex < slList.length) {
                    jQuery('#slIndex').val(slIndex);
                } else {
                    slIndex = 0;
                    jQuery('#slIndex').val(slIndex);

                    tslIndex += 1;
                    if (slIndex < slList.length) {
                        jQuery('#slIndex').val(tslIndex);
                    } else {
                        swal({ title: 'Success', text: 'Backtest completed, all settings were tested!', type: 'success' });
                        return;
                    }
                }
            }

            if (tpList.length > 0) {
                jQuery("#percentage_profit_test").val(tpList[tpIndex]).change();
            }
            if (slList.length > 0) {
                jQuery("#stop_loss_percentage_test").val(slList[slIndex]).change();
            }
            if (tslList.length > 0) {
                const tsl = tslList[tslIndex].split("-");
                jQuery("#stop_loss_trailing_percentage_test").val(tsl[0]).change();
                jQuery("#stop_loss_trailing_arm_test").val(tsl[1]).change();
            }

            const tps = jQuery('#tpList').val().split(",").length;
            const sls = jQuery('#slList').val().split(",").length;
            const tsls = jQuery('#tslList').val().split(",").length;
            const totalBacktests = (tps > 0 ? tps : 1) * (sls > 0 ? sls : 1) * (tsls > 0 ? tsls : 1);
            const current = (tslIndex * sls * tps) + (slIndex * tps) + tpIndex;
            const percent = 100 * current / totalBacktests;
            console.log(current);
            console.log(percent + "% finished, now testing: " + jQuery("#percentage_profit_test").val() + "tp " + jQuery("#stop_loss_percentage_test").val() + "sl " + jQuery("#stop_loss_trailing_percentage_test").val() + "-" + jQuery("#stop_loss_trailing_arm_test").val()+ "tsl");
            setTimeout(function(){ startBackTestConfig(); }, 2000);
        }
    }

    function doBacktestMultipleSettings() {
        swal({
            title: 'TP Options',
            input: 'textarea',
            text: 'Input your tp list, comma seperated',
            inputPlaceholder: '0.4,0.5,1.2 etc.',
            showCancelButton: true,
        }).then((result) => {
            jQuery('#tpList').val(result.value).change();
            jQuery('#tpIndex').val("0").change();
            return swal({
                title: 'SL Options',
                input: 'textarea',
                text: 'Input your sl list, comma seperated',
                inputPlaceholder: '0.4,0.5,1.2 etc.',
                showCancelButton: true,
            });
        }).then((result) => {
            jQuery('#slList').val(result.value).change();
            jQuery('#slIndex').val("0").change();
            return swal({
                title: 'TSL Options',
                input: 'textarea',
                text: 'Input your tsl list, comma seperated. (percent first, arm second)',
                inputPlaceholder: '0.5-1.5,0.3-1.8,0.8-2.5 etc.',
                showCancelButton: true,
            });
        }).then((result) => {
            jQuery('#tslList').val(result.value).change();
            jQuery('#tslIndex').val("0").change();

            const tps = jQuery('#tpList').val().split(",").length;
            const sls = jQuery('#slList').val().split(",").length;
            const tsls = jQuery('#tslList').val().split(",").length;
            const totalBacktests = (tps > 0 ? tps : 1) * (sls > 0 ? sls : 1) * (tsls > 0 ? tsls : 1);

            return swal({
                type: 'question',
                title: 'Continue?',
                text: 'You will run ' + totalBacktests + ' backtests, do you want to continue?',
                showCancelButton: true,
            });
        }).then((result) => {
            var overrideScript = document.createElement('script');
            overrideScript.innerHTML = socketMessagesHandler.toString().replace(/([\s\S]*?return;){2}([\s\S]*)}/,'$2');
            document.body.appendChild(overrideScript);

            setTimeout(function(){ startBackTestConfig(); }, 10);
        });
    }

    function addElements() {
        const backtestTpList = jQuery('<input id="tpList" hidden></input>');
        const backtestTpIndex = jQuery('<input id="tpIndex" hidden></input>');
        const backtestSlList = jQuery('<input id="slList" hidden></input>');
        const backtestSlIndex = jQuery('<input id="slIndex" hidden></input>');
        const backtestTslList = jQuery('<input id="tslList" hidden></input>');
        const backtestTslIndex = jQuery('<input id="tslIndex" hidden></input>');
        const backtestMultipleSettingsButton = jQuery('<button type="button" class="btn btn-success btn-lg">Backtest multiple settings</button>');
        backtestMultipleSettingsButton.on('click', () => doBacktestMultipleSettings());
        jQuery('#backtest-config > div > div:nth-child(20) > div')
            .append(backtestTpList).append(backtestTpIndex)
            .append(backtestSlList).append(backtestSlIndex)
            .append(backtestTslList).append(backtestTslIndex)
            .append(backtestMultipleSettingsButton);

    }

    jQuery(document).ready(() => addElements());
})();

/* AI learn allowed coins forked from 0SkillAllLuck */
/* https://github.com/0SkillAllLuck/cryptohopper_scripts */

(function () {
    'use strict';

    function trainCoinPairs(config, coinPairs, currentQueueSize) {
        if (coinPairs.length < 1) {
            swal({
                title: 'Success',
                text: 'All allowed coins added to training queue!',
                type: 'success',
            });
            return finishTraining(currentQueueSize);
        }

        if (currentQueueSize >= max_trainings) {
            const pairsRemaining = coinPairs.join(', ');
            swal({
                title: 'Full queue',
                text: `Training queue filled up! Remaining coins: ${pairsRemaining}`,
                type: 'error',
            });
            return finishTraining(currentQueueSize);
        }

        const currentCoinPair = coinPairs.pop();
        console.log(`Starting training for coin pair ${currentCoinPair}...`);

        doApiCall(
            'convertmarket',
            {
                exchange: config.exchange,
                market: currentCoinPair,
            },
            (result) => {
                doApiCall(
                    'trainai',
                    {
                        ...config,
                        pair: result.pair,
                    },
                    (_result) => {
                        console.log(`${currentCoinPair} added to training queue`);

                        refreshAITrainings();
                        setTimeout(
                            () => trainCoinPairs(config, coinPairs, currentQueueSize + 1),
                            1200
                        );
                    },
                    (error) => {
                        swal({ title: 'Error', text: error, timer: 4e3, type: 'error' });
                        finishTraining(currentQueueSize);
                    }
                );
            },
            (error) => {
                swal({ title: 'Error', text: error, timer: 4e3, type: 'error' });
                finishTraining(currentQueueSize);
            }
        );
    }

    function startTrainingCoinPairs(coinPairs) {
        const config = {};
        config.id = jQuery('#ai_id').val();
        if (config.id == 'new') {
            return swal({
                title: 'Error',
                text: 'You cannot train a new AI. Please save your AI first.',
                timer: 4e3,
                type: 'error',
            });
        }

        const button = jQuery('#learnAIButton');
        button.html('<i class="fa fa-refresh fa-spin m-r-5"></i>');
        button.prop('disabled', true);

        const strategy = jQuery('#selected_strategy_id option:selected');
        config.exchange = jQuery('#select_exchange').val();
        config.strategy_id = strategy.val();
        config.strategy_type = strategy.data('type');

        // Get training queue and start training
        doApiCall(
            'loadaitraining',
            {
                id: config.id,
            },
            (result) => {
                // Filter out unavailable pairs
                const availablePairs = window
                    .jQuery('#select_market option')
                    .map(function () {
                        return jQuery(this).val();
                    })
                    .get();

                coinPairs = coinPairs.filter((coinPair) => {
                    const splitPair = coinPair.split('/');
                    return (
                        !!availablePairs.find((availablePair) => availablePair === coinPair) &&
                        !result.data.find(
                            (training) =>
                                training.strategy_id == config.strategy_id &&
                                training.exchange == config.exchange &&
                                training.pair.includes(splitPair[0]) &&
                                training.pair.includes(splitPair[1])
                        )
                    );
                });
                console.log('Coins available to train: ', coinPairs.join(', '));

                // Start training
                trainCoinPairs(config, coinPairs, result.total_trainings);
            },
            (error) => {
                swal({ title: 'Error', text: error, timer: 4e3, type: 'error' });
                jQuery('#learnAIButton').html('<i class="md md-android m-r-5"></i> Learn');
            }
        );
    }

    function finishTraining(currentQueueSize) {
        jQuery('#learnAIButton').html('<i class="md md-android m-r-5"></i> Learn');
        return setAILearnButton(currentQueueSize);
    }

    function doTrainAIAllowedCoins() {
        $.get('https://www.cryptohopper.com/config', function(configPage) {
            const base = $(configPage).find('#collect_currency').val().toUpperCase();
            const coinPairList = $(configPage).find('#allowed_coins').val().map((coin) => `${coin}/${base}`);
            startTrainingCoinPairs(coinPairList);
        });
    }

    function addElements() {
        const button = jQuery('<button type="button" class="btn waves-effect waves-light btn-primary" style="margin-top: 15px"><i class="md md-android m-r-5"></i> Learn Allowed Coins</button>');
        const buttonGroup = jQuery('<div class="input-group pull-right"></div>');
        buttonGroup.append(button);

        jQuery('#ai_training > div:nth-child(1) > div > div > div > div.col-md-8.col-lg-9 > div').append(buttonGroup);

        button.on('click', () => doTrainAIAllowedCoins());
    }

    jQuery(document).ready(() => addElements());
})();

/* AI show all markets forked from coffeeneer */
/* https://github.com/coffeeneer/cryptohopper_scripts */

(function () {
  'use strict';

  function showAllMarkets() {
    jQuery('#best_scoring_markets_table tr').show();
  }

  function addElements() {
    const button = jQuery('<a href="#">Show hidden &gt;</a>');
    const col = jQuery('<div class="col-md-12"></div>');
    const row = jQuery('<div class="row"></div>');
    col.append(button);
    row.append(col);

    jQuery('#best_scoring_markets_table').parent().before(row);

    button.on('click', () => showAllMarkets());
  }

  jQuery(document).ready(() => addElements());
})();

/* Export saved trade history forked from falcontx */
/* https://github.com/markrickert/cryptohopper-dashboard-watchlist */

try {
  // Only run this code on the intended page(s) (useful when @required in a parent script)
  if (["/trade-history"].includes(window.location.pathname))
    (function () {
      "use strict";

      const EXPORT_KEY = "export-trade-history-settings";
      const EXPORT_BUTTON_NAME = "#export-saved-trade-history";
      const SAVE_BUTTON_NAME = "#save-export-settings";
      const LOAD_BUTTON_NAME = "#load-export-settings";
      const BUTTON_PRIMARY_CLASS = "btn btn-primary waves-effect waves-light";
      const BUTTON_SECONDARY_CLASS = "btn btn-default waves-effect";
      var buttonsAdded = false;

      // This function loads the currently saved settings
      function loadSavedSettings() {
        var exportSettings = JSON.parse(GM_getValue(EXPORT_KEY));

        // Apply saved settings
        $("#export_type").val(exportSettings.format);
        $("#check_sells").prop("checked", exportSettings.buys);
        $("#check_buys").prop("checked", exportSettings.sells);
        $("#export_daterange").val(exportSettings.daterange);
      }

      // This function sets our CSS
      function setStyles() {
        GM_addStyle(`
        button${EXPORT_BUTTON_NAME},
        button${SAVE_BUTTON_NAME} {
          margin-right: 3px;
        }
        button${LOAD_BUTTON_NAME} {
          margin-right: 2px;
        }
      `);
      }

      // This function adds the Export Saved button and handles click events
      function exportButtonHandler() {
        if (
          !$(EXPORT_BUTTON_NAME).length &&
          GM_getValue(EXPORT_KEY, false) !== false
        ) {
          // Add the Export Saved button
          $(`button[onclick="jQuery('#exportDiv').toggle()"]`).before(
            `<button type="button" id="${EXPORT_BUTTON_NAME.replace(
              "#",
              ""
            )}" class="${BUTTON_PRIMARY_CLASS}"><i class="fa fa-download m-r-5"></i> Export Saved</button>`
          );

          // Handle clicks of the Export Saved button
          $(EXPORT_BUTTON_NAME).on("click", function () {
            loadSavedSettings();

            startExport();
          });

          buttonsAdded = true;
        }
      }

      // This function saves the current settings when exporting
      function saveSettingsButtonHandler() {
        // Add the Save Settings button
        $('button[onclick="startExport()"]').before(
          `<button type="button" id="${SAVE_BUTTON_NAME.replace(
            "#",
            ""
          )}" class="${BUTTON_PRIMARY_CLASS}">Save Settings</button>`
        );

        // Handle clicks of the Save Settings button
        $(SAVE_BUTTON_NAME).on("click", function () {
          var format = $("#export_type").val();
          var buys = $("#check_sells").prop("checked");
          var sells = $("#check_buys").prop("checked");
          var daterange = $("#export_daterange").val();

          // Save these values for future use
          GM_setValue(
            EXPORT_KEY,
            JSON.stringify({
              format: format,
              buys: buys,
              sells: sells,
              daterange: daterange,
            })
          );

          // If this is the first time saving, add the Export Saved and Load Settings buttons
          if (!buttonsAdded) {
            exportButtonHandler();
            loadSettingsButtonHandler();
          }
        });
      }

      // This function loads the currently saved settings
      function loadSettingsButtonHandler() {
        if (
          !$(LOAD_BUTTON_NAME).length &&
          GM_getValue(EXPORT_KEY, false) !== false
        ) {
          // Add the Load Settings button
          $(SAVE_BUTTON_NAME).before(
            `<button type="button" id="${LOAD_BUTTON_NAME.replace(
              "#",
              ""
            )}" class="${BUTTON_SECONDARY_CLASS}">Load Settings</button>`
          );

          // Handle clicks of the Load Settings button
          $(LOAD_BUTTON_NAME).on("click", loadSavedSettings);

          buttonsAdded = true;
        }
      }

      jQuery(() => {
        setStyles();
        exportButtonHandler();
        saveSettingsButtonHandler();
        loadSettingsButtonHandler();
      });
    })();
} catch (err) {
  console.log(
    `Error in script export-saved-trade-history.user.js: ${err.name}: ${err.message}`
  );
}

/* Cryptohopper CSS */
(function () {
    jQuery(() => {
        GM_addStyle(`
      :root {
      --100B:#000 !important;
	  --BRGBA50:rgba(0, 0, 0, .50) !important;
	  --BRGBA25:rgba(0, 0, 0, .25) !important;
      --90B:#1A1A1A !important;
      --80B:#333 !important;
      --70B:#4D4D4D !important;
      --60B:#666 !important;
      --50B:#808080 !important;
      --40B:#999 !important;
      --30B:#B3B3B3 !important;
      --20B:#CCC !important;
      --10B:#E6E6E6 !important;
	  --WRGBA50:rgba(255, 255, 255, .50) !important;
      --00B:#FFF !important;
	  --WRGBA25:rgba(255, 255, 255, .25) !important;
      --HB:#00B2C8 !important;
	  --HBRGBA50:rgba(0, 178, 200, .50) !important;
	  --HBRGBA25:rgba(0, 178, 200, .25) !important;
	  --RED:#FF0040 !important;
	  --REDRGBA50:rgba(255, 0, 64, .50) !important;
	  --REDRGBA25:rgba(255, 0, 64, .25) !important;
	  --GRN:#00C757 !important;
	  --GRNRGBA50:rgba(0, 199, 87, .50) !important;
	  --GRNRGBA25:rgba(0, 199, 87, .25) !important;
	  --ORG:#FF980B !important;
	  --ORGRGBA50:rgba(255, 152, 11, .50) !important;
	  --ORGRGBA25:rgba(255, 152, 11, .25) !important;
	  --PUR:#A53F98 !important;
	  --PURRGBA50:rgba(165, 63, 152, .50) !important;
	  --PURRGBA25:rgba(165, 63, 152, .25) !important;
	  --PIN:#FF5586 !important;
	  --PINRGBA50:rgba(255, 85, 134, .50) !important;
	  --PINRGBA25:rgba(255, 85, 134, .25) !important;
	  --SliderColor_GRN: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAQQAAACoCAYAAAAGoZArAAAKN2lDQ1BzUkdCIElFQzYxOTY2LTIuMQAAeJydlndUU9kWh8+9N71QkhCKlNBraFICSA29SJEuKjEJEErAkAAiNkRUcERRkaYIMijggKNDkbEiioUBUbHrBBlE1HFwFBuWSWStGd+8ee/Nm98f935rn73P3Wfvfda6AJD8gwXCTFgJgAyhWBTh58WIjYtnYAcBDPAAA2wA4HCzs0IW+EYCmQJ82IxsmRP4F726DiD5+yrTP4zBAP+flLlZIjEAUJiM5/L42VwZF8k4PVecJbdPyZi2NE3OMErOIlmCMlaTc/IsW3z2mWUPOfMyhDwZy3PO4mXw5Nwn4405Er6MkWAZF+cI+LkyviZjg3RJhkDGb+SxGXxONgAoktwu5nNTZGwtY5IoMoIt43kA4EjJX/DSL1jMzxPLD8XOzFouEiSniBkmXFOGjZMTi+HPz03ni8XMMA43jSPiMdiZGVkc4XIAZs/8WRR5bRmyIjvYODk4MG0tbb4o1H9d/JuS93aWXoR/7hlEH/jD9ld+mQ0AsKZltdn6h21pFQBd6wFQu/2HzWAvAIqyvnUOfXEeunxeUsTiLGcrq9zcXEsBn2spL+jv+p8Of0NffM9Svt3v5WF485M4knQxQ143bmZ6pkTEyM7icPkM5p+H+B8H/nUeFhH8JL6IL5RFRMumTCBMlrVbyBOIBZlChkD4n5r4D8P+pNm5lona+BHQllgCpSEaQH4eACgqESAJe2Qr0O99C8ZHA/nNi9GZmJ37z4L+fVe4TP7IFiR/jmNHRDK4ElHO7Jr8WgI0IABFQAPqQBvoAxPABLbAEbgAD+ADAkEoiARxYDHgghSQAUQgFxSAtaAYlIKtYCeoBnWgETSDNnAYdIFj4DQ4By6By2AE3AFSMA6egCnwCsxAEISFyBAVUod0IEPIHLKFWJAb5AMFQxFQHJQIJUNCSAIVQOugUqgcqobqoWboW+godBq6AA1Dt6BRaBL6FXoHIzAJpsFasBFsBbNgTzgIjoQXwcnwMjgfLoK3wJVwA3wQ7oRPw5fgEVgKP4GnEYAQETqiizARFsJGQpF4JAkRIauQEqQCaUDakB6kH7mKSJGnyFsUBkVFMVBMlAvKHxWF4qKWoVahNqOqUQdQnag+1FXUKGoK9RFNRmuizdHO6AB0LDoZnYsuRlegm9Ad6LPoEfQ4+hUGg6FjjDGOGH9MHCYVswKzGbMb0445hRnGjGGmsVisOtYc64oNxXKwYmwxtgp7EHsSewU7jn2DI+J0cLY4X1w8TogrxFXgWnAncFdwE7gZvBLeEO+MD8Xz8MvxZfhGfA9+CD+OnyEoE4wJroRIQiphLaGS0EY4S7hLeEEkEvWITsRwooC4hlhJPEQ8TxwlviVRSGYkNimBJCFtIe0nnSLdIr0gk8lGZA9yPFlM3kJuJp8h3ye/UaAqWCoEKPAUVivUKHQqXFF4pohXNFT0VFysmK9YoXhEcUjxqRJeyUiJrcRRWqVUo3RU6YbStDJV2UY5VDlDebNyi/IF5UcULMWI4kPhUYoo+yhnKGNUhKpPZVO51HXURupZ6jgNQzOmBdBSaaW0b2iDtCkVioqdSrRKnkqNynEVKR2hG9ED6On0Mvph+nX6O1UtVU9Vvuom1TbVK6qv1eaoeajx1UrU2tVG1N6pM9R91NPUt6l3qd/TQGmYaYRr5Grs0Tir8XQObY7LHO6ckjmH59zWhDXNNCM0V2ju0xzQnNbS1vLTytKq0jqj9VSbru2hnaq9Q/uE9qQOVcdNR6CzQ+ekzmOGCsOTkc6oZPQxpnQ1df11Jbr1uoO6M3rGelF6hXrtevf0Cfos/ST9Hfq9+lMGOgYhBgUGrQa3DfGGLMMUw12G/YavjYyNYow2GHUZPTJWMw4wzjduNb5rQjZxN1lm0mByzRRjyjJNM91tetkMNrM3SzGrMRsyh80dzAXmu82HLdAWThZCiwaLG0wS05OZw2xljlrSLYMtCy27LJ9ZGVjFW22z6rf6aG1vnW7daH3HhmITaFNo02Pzq62ZLde2xvbaXPJc37mr53bPfW5nbse322N3055qH2K/wb7X/oODo4PIoc1h0tHAMdGx1vEGi8YKY21mnXdCO3k5rXY65vTW2cFZ7HzY+RcXpkuaS4vLo3nG8/jzGueNueq5clzrXaVuDLdEt71uUnddd457g/sDD30PnkeTx4SnqWeq50HPZ17WXiKvDq/XbGf2SvYpb8Tbz7vEe9CH4hPlU+1z31fPN9m31XfKz95vhd8pf7R/kP82/xsBWgHcgOaAqUDHwJWBfUGkoAVB1UEPgs2CRcE9IXBIYMj2kLvzDecL53eFgtCA0O2h98KMw5aFfR+OCQ8Lrwl/GGETURDRv4C6YMmClgWvIr0iyyLvRJlESaJ6oxWjE6Kbo1/HeMeUx0hjrWJXxl6K04gTxHXHY+Oj45vipxf6LNy5cDzBPqE44foi40V5iy4s1licvvj4EsUlnCVHEtGJMYktie85oZwGzvTSgKW1S6e4bO4u7hOeB28Hb5Lvyi/nTyS5JpUnPUp2Td6ePJninlKR8lTAFlQLnqf6p9alvk4LTduf9ik9Jr09A5eRmHFUSBGmCfsytTPzMoezzLOKs6TLnJftXDYlChI1ZUPZi7K7xTTZz9SAxESyXjKa45ZTk/MmNzr3SJ5ynjBvYLnZ8k3LJ/J9879egVrBXdFboFuwtmB0pefK+lXQqqWrelfrry5aPb7Gb82BtYS1aWt/KLQuLC98uS5mXU+RVtGaorH1futbixWKRcU3NrhsqNuI2ijYOLhp7qaqTR9LeCUXS61LK0rfb+ZuvviVzVeVX33akrRlsMyhbM9WzFbh1uvb3LcdKFcuzy8f2x6yvXMHY0fJjpc7l+y8UGFXUbeLsEuyS1oZXNldZVC1tep9dUr1SI1XTXutZu2m2te7ebuv7PHY01anVVda926vYO/Ner/6zgajhop9mH05+x42Rjf2f836urlJo6m06cN+4X7pgYgDfc2Ozc0tmi1lrXCrpHXyYMLBy994f9Pdxmyrb6e3lx4ChySHHn+b+O31w0GHe4+wjrR9Z/hdbQe1o6QT6lzeOdWV0iXtjusePhp4tLfHpafje8vv9x/TPVZzXOV42QnCiaITn07mn5w+lXXq6enk02O9S3rvnIk9c60vvG/wbNDZ8+d8z53p9+w/ed71/LELzheOXmRd7LrkcKlzwH6g4wf7HzoGHQY7hxyHui87Xe4Znjd84or7ldNXva+euxZw7dLI/JHh61HXb95IuCG9ybv56Fb6ree3c27P3FlzF3235J7SvYr7mvcbfjT9sV3qID0+6j068GDBgztj3LEnP2X/9H686CH5YcWEzkTzI9tHxyZ9Jy8/Xvh4/EnWk5mnxT8r/1z7zOTZd794/DIwFTs1/lz0/NOvm1+ov9j/0u5l73TY9P1XGa9mXpe8UX9z4C3rbf+7mHcTM7nvse8rP5h+6PkY9PHup4xPn34D94Tz+49wZioAAAAJcEhZcwAACusAAArrAYKLDVoAAAKdSURBVHic7d0xjtNAGIDRWJoWCYotItFvl3rvQI20R+BIHAGJmjtsnY4epUkBEgcw6wBfmTK2lPcaJ1X+6tN4NLHH6XSadwCvxtoDANshCEAEAYggABEEIIIARBCACAIQQQAiCEAEAcjY7/fT2kMA22CFAEQQgAgCEEEAIghABAGIIAARBCCCAEQQgAgCEEEAIghABAGIIAARBCCCAOQShOPxOD88PKw9C7CS8/m8OxwO0xADYGnA0oIhBsBiaYE9BCCCAEQQgAgCEEEAIghABAHIWE4oOYsALC0Yy3FFpxXhvnV0efmyfFh7IGA9+/3+crWHAEQQgAgCEEEAIghABAGIIAARBCCCAEQQgAgCEEEAIghABAGIIAARBCCCAGRML8/z2kMA22CFAEQQgAgCEEEAIghABAGIIAARBCCCAEQQgAgCkDE/ffHmZ+DCCgGIIAARBCCCAEQQgAgCEEEAIghABAGIIAARBCCCAEQQgAgCEEEAIghABAHIJQjTz0/z7vuvm/6wJzXB9ow1YgBs0xAD4D97CEAEAYggABEEIIIARBCACAKQsXt8u3MWAViM+d3naXp0WhH4d8uwRGH3tPYowNrsIQARBCCCAEQQgAgCEEEAIghABAGIIAARBCCCAEQQgAgCEEEAIghABAGIIAC5GoTp5Xlert7UDPfh+grhx+8bjQFsgVsGIIIARBCACAIQQQAiCEAEAYggABEEIIIARBCACAIQQQAiCEAEAcj1ILx/c6MxgC24GgRPSoL74pYBiCAAEQQgggBEEIAIAhBBACIIQAQBiCAAEQQg19/+/PXD37c/f/zmPw1wB6wQgAgCEEEAIghABAGIIAARBCCCAEQQgAgCEEEAIghABAGIIAARBCCCAEQQgPwBXIlIUf0+LdwAAAAASUVORK5CYII=") !important;
	  --SliderColor_RED: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAQQAAACoCAYAAAAGoZArAAAKN2lDQ1BzUkdCIElFQzYxOTY2LTIuMQAAeJydlndUU9kWh8+9N71QkhCKlNBraFICSA29SJEuKjEJEErAkAAiNkRUcERRkaYIMijggKNDkbEiioUBUbHrBBlE1HFwFBuWSWStGd+8ee/Nm98f935rn73P3Wfvfda6AJD8gwXCTFgJgAyhWBTh58WIjYtnYAcBDPAAA2wA4HCzs0IW+EYCmQJ82IxsmRP4F726DiD5+yrTP4zBAP+flLlZIjEAUJiM5/L42VwZF8k4PVecJbdPyZi2NE3OMErOIlmCMlaTc/IsW3z2mWUPOfMyhDwZy3PO4mXw5Nwn4405Er6MkWAZF+cI+LkyviZjg3RJhkDGb+SxGXxONgAoktwu5nNTZGwtY5IoMoIt43kA4EjJX/DSL1jMzxPLD8XOzFouEiSniBkmXFOGjZMTi+HPz03ni8XMMA43jSPiMdiZGVkc4XIAZs/8WRR5bRmyIjvYODk4MG0tbb4o1H9d/JuS93aWXoR/7hlEH/jD9ld+mQ0AsKZltdn6h21pFQBd6wFQu/2HzWAvAIqyvnUOfXEeunxeUsTiLGcrq9zcXEsBn2spL+jv+p8Of0NffM9Svt3v5WF485M4knQxQ143bmZ6pkTEyM7icPkM5p+H+B8H/nUeFhH8JL6IL5RFRMumTCBMlrVbyBOIBZlChkD4n5r4D8P+pNm5lona+BHQllgCpSEaQH4eACgqESAJe2Qr0O99C8ZHA/nNi9GZmJ37z4L+fVe4TP7IFiR/jmNHRDK4ElHO7Jr8WgI0IABFQAPqQBvoAxPABLbAEbgAD+ADAkEoiARxYDHgghSQAUQgFxSAtaAYlIKtYCeoBnWgETSDNnAYdIFj4DQ4By6By2AE3AFSMA6egCnwCsxAEISFyBAVUod0IEPIHLKFWJAb5AMFQxFQHJQIJUNCSAIVQOugUqgcqobqoWboW+godBq6AA1Dt6BRaBL6FXoHIzAJpsFasBFsBbNgTzgIjoQXwcnwMjgfLoK3wJVwA3wQ7oRPw5fgEVgKP4GnEYAQETqiizARFsJGQpF4JAkRIauQEqQCaUDakB6kH7mKSJGnyFsUBkVFMVBMlAvKHxWF4qKWoVahNqOqUQdQnag+1FXUKGoK9RFNRmuizdHO6AB0LDoZnYsuRlegm9Ad6LPoEfQ4+hUGg6FjjDGOGH9MHCYVswKzGbMb0445hRnGjGGmsVisOtYc64oNxXKwYmwxtgp7EHsSewU7jn2DI+J0cLY4X1w8TogrxFXgWnAncFdwE7gZvBLeEO+MD8Xz8MvxZfhGfA9+CD+OnyEoE4wJroRIQiphLaGS0EY4S7hLeEEkEvWITsRwooC4hlhJPEQ8TxwlviVRSGYkNimBJCFtIe0nnSLdIr0gk8lGZA9yPFlM3kJuJp8h3ye/UaAqWCoEKPAUVivUKHQqXFF4pohXNFT0VFysmK9YoXhEcUjxqRJeyUiJrcRRWqVUo3RU6YbStDJV2UY5VDlDebNyi/IF5UcULMWI4kPhUYoo+yhnKGNUhKpPZVO51HXURupZ6jgNQzOmBdBSaaW0b2iDtCkVioqdSrRKnkqNynEVKR2hG9ED6On0Mvph+nX6O1UtVU9Vvuom1TbVK6qv1eaoeajx1UrU2tVG1N6pM9R91NPUt6l3qd/TQGmYaYRr5Grs0Tir8XQObY7LHO6ckjmH59zWhDXNNCM0V2ju0xzQnNbS1vLTytKq0jqj9VSbru2hnaq9Q/uE9qQOVcdNR6CzQ+ekzmOGCsOTkc6oZPQxpnQ1df11Jbr1uoO6M3rGelF6hXrtevf0Cfos/ST9Hfq9+lMGOgYhBgUGrQa3DfGGLMMUw12G/YavjYyNYow2GHUZPTJWMw4wzjduNb5rQjZxN1lm0mByzRRjyjJNM91tetkMNrM3SzGrMRsyh80dzAXmu82HLdAWThZCiwaLG0wS05OZw2xljlrSLYMtCy27LJ9ZGVjFW22z6rf6aG1vnW7daH3HhmITaFNo02Pzq62ZLde2xvbaXPJc37mr53bPfW5nbse322N3055qH2K/wb7X/oODo4PIoc1h0tHAMdGx1vEGi8YKY21mnXdCO3k5rXY65vTW2cFZ7HzY+RcXpkuaS4vLo3nG8/jzGueNueq5clzrXaVuDLdEt71uUnddd457g/sDD30PnkeTx4SnqWeq50HPZ17WXiKvDq/XbGf2SvYpb8Tbz7vEe9CH4hPlU+1z31fPN9m31XfKz95vhd8pf7R/kP82/xsBWgHcgOaAqUDHwJWBfUGkoAVB1UEPgs2CRcE9IXBIYMj2kLvzDecL53eFgtCA0O2h98KMw5aFfR+OCQ8Lrwl/GGETURDRv4C6YMmClgWvIr0iyyLvRJlESaJ6oxWjE6Kbo1/HeMeUx0hjrWJXxl6K04gTxHXHY+Oj45vipxf6LNy5cDzBPqE44foi40V5iy4s1licvvj4EsUlnCVHEtGJMYktie85oZwGzvTSgKW1S6e4bO4u7hOeB28Hb5Lvyi/nTyS5JpUnPUp2Td6ePJninlKR8lTAFlQLnqf6p9alvk4LTduf9ik9Jr09A5eRmHFUSBGmCfsytTPzMoezzLOKs6TLnJftXDYlChI1ZUPZi7K7xTTZz9SAxESyXjKa45ZTk/MmNzr3SJ5ynjBvYLnZ8k3LJ/J9879egVrBXdFboFuwtmB0pefK+lXQqqWrelfrry5aPb7Gb82BtYS1aWt/KLQuLC98uS5mXU+RVtGaorH1futbixWKRcU3NrhsqNuI2ijYOLhp7qaqTR9LeCUXS61LK0rfb+ZuvviVzVeVX33akrRlsMyhbM9WzFbh1uvb3LcdKFcuzy8f2x6yvXMHY0fJjpc7l+y8UGFXUbeLsEuyS1oZXNldZVC1tep9dUr1SI1XTXutZu2m2te7ebuv7PHY01anVVda926vYO/Ner/6zgajhop9mH05+x42Rjf2f836urlJo6m06cN+4X7pgYgDfc2Ozc0tmi1lrXCrpHXyYMLBy994f9Pdxmyrb6e3lx4ChySHHn+b+O31w0GHe4+wjrR9Z/hdbQe1o6QT6lzeOdWV0iXtjusePhp4tLfHpafje8vv9x/TPVZzXOV42QnCiaITn07mn5w+lXXq6enk02O9S3rvnIk9c60vvG/wbNDZ8+d8z53p9+w/ed71/LELzheOXmRd7LrkcKlzwH6g4wf7HzoGHQY7hxyHui87Xe4Znjd84or7ldNXva+euxZw7dLI/JHh61HXb95IuCG9ybv56Fb6ree3c27P3FlzF3235J7SvYr7mvcbfjT9sV3qID0+6j068GDBgztj3LEnP2X/9H686CH5YcWEzkTzI9tHxyZ9Jy8/Xvh4/EnWk5mnxT8r/1z7zOTZd794/DIwFTs1/lz0/NOvm1+ov9j/0u5l73TY9P1XGa9mXpe8UX9z4C3rbf+7mHcTM7nvse8rP5h+6PkY9PHup4xPn34D94Tz+49wZioAAAAJcEhZcwAACusAAArrAYKLDVoAAAKTSURBVHic7d2xjRNBAEDRXWnowIfkAEpwBSRXBTVSBQkVuASQHGA6IFjYPd0PHXot+b1k7cgTfc2MxjvjcrksE8B/Y+8BAI9DEIAIAhBBACIIQAQBiCAAEQQgggBEEIAIApBxPB7nvQcBPAYzBCCCAEQQgAgCEEEAIghABAGIIAARBCCCAEQQgAgCEEEAIghABAGIIAARBCBbEM7n8/Ly8rL3WICdXK/X6XQ6zUMMgLUBawuGGACrtQX2EIAIAhBBACIIQAQBiCAAEQQgYz2h5CwCsLZgrMcVnVaE59bR5fXL+mHvAQH7OR6P29MeAhBBACIIQAQBiCAAEQQgggBEEIAIAhBBACIIQAQBiCAAEQQgggBEEIAIApAxza/L3oMAHoMZAhBBACIIQAQBiCAAEQQgggBEEIAIAhBBACIIQMa0fHfzM7AxQwAiCEAEAYggABEEIIIARBCACAIQQQAiCEAEAYggABEEIIIARBCACAIQQQDyFoTPX5fp1+/7/rI3NcHDGbvEAHhIQwyAd/YQgAgCEEEAIghABAGIIAARBCBj+vRxchYBWI3p57fZaUVg9bZkWKMAPD17CEAEAYggABEEIIIARBCACAIQQQAiCEAEAYggABEEIIIARBCACAIQQQAiCEBuB2F+Xbanm5rhKdwMwp/p7/Y83GUowN4sGYAIAhBBACIIQAQBiCAAEQQgggBEEIAIAhBBACIIQAQBiCAAEQQgN4NwmD7caxzAA7g9Q/CmJHgqlgxABAGIIAARBCCCAEQQgAgCEEEAIghABAGIIAC5fdnr/GW7/fmw/PCfBngCZghABAGIIAARBCCCAEQQgAgCEEEAIghABAGIIAARBCCCAEQQgAgCEEEAIghA/gHrv0Pgt+gJBgAAAABJRU5ErkJggg==") !important;
	  --SliderColor_HB: url("data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAQQAAACoCAYAAAAGoZArAAAABGdBTUEAALGOfPtRkwAAACBjSFJNAACHDwAAjA8AAP1SAACBQAAAfXkAAOmLAAA85QAAGcxzPIV3AAAKL2lDQ1BJQ0MgUHJvZmlsZQAASMedlndUVNcWh8+9d3qhzTDSGXqTLjCA9C4gHQRRGGYGGMoAwwxNbIioQEQREQFFkKCAAaOhSKyIYiEoqGAPSBBQYjCKqKhkRtZKfHl57+Xl98e939pn73P32XuftS4AJE8fLi8FlgIgmSfgB3o401eFR9Cx/QAGeIABpgAwWempvkHuwUAkLzcXerrICfyL3gwBSPy+ZejpT6eD/0/SrFS+AADIX8TmbE46S8T5Ik7KFKSK7TMipsYkihlGiZkvSlDEcmKOW+Sln30W2VHM7GQeW8TinFPZyWwx94h4e4aQI2LER8QFGVxOpohvi1gzSZjMFfFbcWwyh5kOAIoktgs4rHgRm4iYxA8OdBHxcgBwpLgvOOYLFnCyBOJDuaSkZvO5cfECui5Lj25qbc2ge3IykzgCgaE/k5XI5LPpLinJqUxeNgCLZ/4sGXFt6aIiW5paW1oamhmZflGo/7r4NyXu7SK9CvjcM4jW94ftr/xS6gBgzIpqs+sPW8x+ADq2AiB3/w+b5iEAJEV9a7/xxXlo4nmJFwhSbYyNMzMzjbgclpG4oL/rfzr8DX3xPSPxdr+Xh+7KiWUKkwR0cd1YKUkpQj49PZXJ4tAN/zzE/zjwr/NYGsiJ5fA5PFFEqGjKuLw4Ubt5bK6Am8Kjc3n/qYn/MOxPWpxrkSj1nwA1yghI3aAC5Oc+gKIQARJ5UNz13/vmgw8F4psXpjqxOPefBf37rnCJ+JHOjfsc5xIYTGcJ+RmLa+JrCdCAACQBFcgDFaABdIEhMANWwBY4AjewAviBYBAO1gIWiAfJgA8yQS7YDApAEdgF9oJKUAPqQSNoASdABzgNLoDL4Dq4Ce6AB2AEjIPnYAa8AfMQBGEhMkSB5CFVSAsygMwgBmQPuUE+UCAUDkVDcRAPEkK50BaoCCqFKqFaqBH6FjoFXYCuQgPQPWgUmoJ+hd7DCEyCqbAyrA0bwwzYCfaGg+E1cBycBufA+fBOuAKug4/B7fAF+Dp8Bx6Bn8OzCECICA1RQwwRBuKC+CERSCzCRzYghUg5Uoe0IF1IL3ILGUGmkXcoDIqCoqMMUbYoT1QIioVKQ21AFaMqUUdR7age1C3UKGoG9QlNRiuhDdA2aC/0KnQcOhNdgC5HN6Db0JfQd9Dj6DcYDIaG0cFYYTwx4ZgEzDpMMeYAphVzHjOAGcPMYrFYeawB1g7rh2ViBdgC7H7sMew57CB2HPsWR8Sp4sxw7rgIHA+XhyvHNeHO4gZxE7h5vBReC2+D98Oz8dn4Enw9vgt/Az+OnydIE3QIdoRgQgJhM6GC0EK4RHhIeEUkEtWJ1sQAIpe4iVhBPE68QhwlviPJkPRJLqRIkpC0k3SEdJ50j/SKTCZrkx3JEWQBeSe5kXyR/Jj8VoIiYSThJcGW2ChRJdEuMSjxQhIvqSXpJLlWMkeyXPKk5A3JaSm8lLaUixRTaoNUldQpqWGpWWmKtKm0n3SydLF0k/RV6UkZrIy2jJsMWyZf5rDMRZkxCkLRoLhQWJQtlHrKJco4FUPVoXpRE6hF1G+o/dQZWRnZZbKhslmyVbJnZEdoCE2b5kVLopXQTtCGaO+XKC9xWsJZsmNJy5LBJXNyinKOchy5QrlWuTty7+Xp8m7yifK75TvkHymgFPQVAhQyFQ4qXFKYVqQq2iqyFAsVTyjeV4KV9JUCldYpHVbqU5pVVlH2UE5V3q98UXlahabiqJKgUqZyVmVKlaJqr8pVLVM9p/qMLkt3oifRK+g99Bk1JTVPNaFarVq/2ry6jnqIep56q/ojDYIGQyNWo0yjW2NGU1XTVzNXs1nzvhZei6EVr7VPq1drTltHO0x7m3aH9qSOnI6XTo5Os85DXbKug26abp3ubT2MHkMvUe+A3k19WN9CP16/Sv+GAWxgacA1OGAwsBS91Hopb2nd0mFDkqGTYYZhs+GoEc3IxyjPqMPohbGmcYTxbuNe408mFiZJJvUmD0xlTFeY5pl2mf5qpm/GMqsyu21ONnc332jeaf5ymcEyzrKDy+5aUCx8LbZZdFt8tLSy5Fu2WE5ZaVpFW1VbDTOoDH9GMeOKNdra2Xqj9WnrdzaWNgKbEza/2BraJto22U4u11nOWV6/fMxO3Y5pV2s3Yk+3j7Y/ZD/ioObAdKhzeOKo4ch2bHCccNJzSnA65vTC2cSZ79zmPOdi47Le5bwr4urhWuja7ybjFuJW6fbYXd09zr3ZfcbDwmOdx3lPtKe3527PYS9lL5ZXo9fMCqsV61f0eJO8g7wrvZ/46Pvwfbp8Yd8Vvnt8H67UWslb2eEH/Lz89vg98tfxT/P/PgAT4B9QFfA00DQwN7A3iBIUFdQU9CbYObgk+EGIbogwpDtUMjQytDF0Lsw1rDRsZJXxqvWrrocrhHPDOyOwEaERDRGzq91W7109HmkRWRA5tEZnTdaaq2sV1iatPRMlGcWMOhmNjg6Lbor+wPRj1jFnY7xiqmNmWC6sfaznbEd2GXuKY8cp5UzE2sWWxk7G2cXtiZuKd4gvj5/munAruS8TPBNqEuYS/RKPJC4khSW1JuOSo5NP8WR4ibyeFJWUrJSBVIPUgtSRNJu0vWkzfG9+QzqUvia9U0AV/Uz1CXWFW4WjGfYZVRlvM0MzT2ZJZ/Gy+rL1s3dkT+S453y9DrWOta47Vy13c+7oeqf1tRugDTEbujdqbMzfOL7JY9PRzYTNiZt/yDPJK817vSVsS1e+cv6m/LGtHlubCyQK+AXD22y31WxHbedu799hvmP/jk+F7MJrRSZF5UUfilnF174y/ariq4WdsTv7SyxLDu7C7OLtGtrtsPtoqXRpTunYHt897WX0ssKy13uj9l4tX1Zes4+wT7hvpMKnonO/5v5d+z9UxlfeqXKuaq1Wqt5RPXeAfWDwoOPBlhrlmqKa94e4h+7WetS212nXlR/GHM44/LQ+tL73a8bXjQ0KDUUNH4/wjowcDTza02jV2Nik1FTSDDcLm6eORR67+Y3rN50thi21rbTWouPguPD4s2+jvx064X2i+yTjZMt3Wt9Vt1HaCtuh9uz2mY74jpHO8M6BUytOdXfZdrV9b/T9kdNqp6vOyJ4pOUs4m3924VzOudnzqeenL8RdGOuO6n5wcdXF2z0BPf2XvC9duex++WKvU++5K3ZXTl+1uXrqGuNax3XL6+19Fn1tP1j80NZv2d9+w+pG503rm10DywfODjoMXrjleuvyba/b1++svDMwFDJ0dzhyeOQu++7kvaR7L+9n3J9/sOkh+mHhI6lH5Y+VHtf9qPdj64jlyJlR19G+J0FPHoyxxp7/lP7Th/H8p+Sn5ROqE42TZpOnp9ynbj5b/Wz8eerz+emCn6V/rn6h++K7Xxx/6ZtZNTP+kv9y4dfiV/Kvjrxe9rp71n/28ZvkN/NzhW/l3x59x3jX+z7s/cR85gfsh4qPeh+7Pnl/eriQvLDwG/eE8/s3BCkeAAAACXBIWXMAAArrAAAK6wGCiw1aAAAAIXRFWHRDcmVhdGlvbiBUaW1lADIwMjE6MDY6MTYgMTg6NDY6MTCRt03qAAACfUlEQVR4Xu3dMaoTQQCA4Z09gpBKECzsJK2n8H6ewVIvoWWCnYUguE3AK6wvyb7fLqU+Xr4PhuzuAX5mh8nsWJZlnQAezNsvgCAAfwkCEEEAIghABAGIIAARBCCCAEQQgAgCkLGu/soAXJkhABEEIIIARBCACAIQQQAiCEAEAYggABEEIIIARBCACAIQQQAiCEAEAYggALmcmHQ8Htfdbrc9Au7N6XSa9vv9GIfDQQyASxTGsiwOVQQurCEAEQQgggBEEIAIAhBBACIIQObzZgSAcwvm83ZFUYD71tZlX38GHllDACIIQAQBiCAAEQQgggBEEIAIAhBBACIIQAQBiCAAEQQgggBEEIAIAhBBADKmT18cmQRcmCEAEQQgggBEEIAIAhBBACIIQAQBiCAAEQQgggDE15+BmCEAEQQgggBEEIAIAhBBACIIQAQBiCAAEQQgggBEEIAIAhBBACIIQAQBiCAAuZyYNL79Xqcf37dH/8b6/t3YLoEnYv4fMQCeplkMgEfWEIAIAhBBACIIQAQBiCAAEQQg8/T6zXYJ3Lt5fftiiAJw5uvPQKwhABEEIIIARBCACAIQQQAiCEAEAYggABEEIIIARBCACAIQQQAiCEAEAYggALkZhPH563oe2y3wzN2eIfz6eR3AXfDKAEQQgAgCEEEAIghABAGIIAARBCCCAEQQgAgCEEEAIghABAGIIAC5HYSXr64DuAtjXR2IBFx5ZQAiCEAEAYggABEEIIIARBCACAIQQQAiCEAEAcjNIIwPH9fz2G6BZ84MAYggABEEIIIARBCACAIQQQAiCEAEAYggABEEIIIARBCACAIQQQAiCEAEAdhM0x+J0FUUwHtgzwAAAABJRU5ErkJggg==") !important;
            }
body.nightmode {
    background:var(--70B) !important;
    color:var(--10B) !important;
}
body.nightmode .popover-content {
    color:#000;
}
html.nightmode {
    background:var(--100B) !important;
}
body.nightmode .navbar-default {
    background-color:var(--100B) !important;
	box-shadow:0px 3px 3px rgb(0 0 0/20%) !important;
}
body.nightmode .button-menu-mobile {
    color:var(--10B);
}
.button-menu-mobile:hover {
    color:var(--00B);
}
body.nightmode .navbar-default .navbar-nav>li>a { /* remove "!important" on server CSS for transition */
    color:var(--10B) !important;
}
body.nightmode .navbar-default .navbar-nav>li>a:focus, .navbar-default .navbar-nav>li>a:hover { /* remove "!important" on server CSS for transition */
    color:var(--00B) !important;
}
body.nightmode .forumpage {
    background:#617385;
    color:#F2F2F2;
}
html.nightmode.forumpage {
    background:#617385;
}
body.nightmode .forumpage.phpbb {
    color:var(--10B) !important;
}
body.nightmode h1, h2, h3, h4, h5, h6 {
    color:var(--10B) !important;
}
body.nightmode a {
    color:var(--HB) !important;
}
body.nightmode a:focus, body.nightmode a:hover {
    color:var(--00B) !important;
	will-change:opacity, transform;
    -webkit-transition:all.3s ease-out;
    -moz-transition:all.3s ease-out;
    -o-transition:all.3s ease-out;
    -ms-transition:all.3s ease-out;
    transition:all.3s ease-out;
}
body.nightmode h1 small, h2 small, h3 small, h4 small, h5 small, h6 small {
    color:rgba(255, 255, 255, .5)
}
body.nightmode .footer {
    background-color:var(--90B) !important;
    border-top:1px solid rgba(0, 0, 0, .1);
    color:var(--10B) !important;
}
body.nightmode .well {
    background-color:var(--80B) !important;
    border:1px solid var(--50B);
	box-shadow:none !important;
}
body.nightmode #hopperOutputTableHolder {
    border:1px solid var(--50B) !important;
	box-shadow:none !important;
}
body.nightmode legend {
    color:#98a6ad;
    border-bottom:1px solid #98a6ad;
}
body.nightmode .page-header {
    border-bottom:1px solid rgba(238, 238, 238, .2)
}
body.nightmode .page-title-box.breadcrumb a {
    color:var(--HB) !important;
}
body.nightmode .page-title-box.breadcrumb>.active {
    color:#98a6ad
}
body.nightmode .social-links li a {
    background:#EFF0F4;
    color:#7A7676
}
body.nightmode .breadcrumb {
    background-color:transparent
}
body.nightmode .dropdown-menu {
    background-color:#1c2127;
    box-shadow:0 2px 5px 0 rgba(0, 0, 0, .26);
}
body.nightmode .dropdown-menu>li>a {
    color:#98a6ad
}
body.nightmode .dropdown-menu.divider {
    background-color:rgba(238, 238, 238, .2)
}
body.nightmode .dropdown-menu>li>a:focus, .dropdown-menu>li>a:hover {
    color:rgba(255, 255, 255, .7);
    background-color:#121518
}
body.nightmode hr {
    border-top:1px solid var(--50B) !important;
	margin-top:15px;
    margin-bottom:15px;
    margin-inline-start:0;
    margin-inline-end:0;
}
body.nightmode code {
    color:var(--HB) !important;
}
body.nightmode code, pre {
    background-color:rgba(0, 0, 0, .1);
}
body.nightmode pre {
    background-color:#21272c;
    color:#eee;
    border:1px solid rgba(238, 238, 238, .3);
}
body.nightmode .bg-empty {
    background:0 !important;
}
body.nightmode .bg-primary {
    background-color:var(--HB) !important;
}
body.nightmode .bg-success {
    background-color:var(--GRN) !important;
}
body.nightmode .bg-info {
    background-color:var(--HB) !important;
}
body.nightmode .bg-warning {
    background-color:var(--ORG) !important;
}
body.nightmode .bg-danger {
    background-color:var(--RED) !important;
}
body.nightmode .bg-inverse {
    background-color:var(--HB) !important;
}
body.nightmode .bg-purple {
    background-color:var(--PUR) !important;
}
body.nightmode .bg-pink {
    background-color:var(--PIN) !important;
}
body.nightmode .bg-white {
    background-color: var(--10B) !important;
}
body.nightmode .text-white {
    color:var(--10B) !important;
}
body.nightmode .text-danger {
    color:var(--RED) !important;
}
body.nightmode .text-primary {
    color:var(--HB) !important;
}
body.nightmode .text-warning {
    color:var(--ORG) !important;
}
body.nightmode .text-success {
    color:var(--GRN) !important;
}
body.nightmode .text-info {
    color:var(--HB) !important;
}
body.nightmode .text-inverse {
    color:var(--HB) !important;
}
body.nightmode .text-pink {
    color:var(--PIN) !important;
}
body.nightmode .text-purple {
    color:var(--PUR) !important;
}
body.nightmode .span.switchery.switchery-default.text-success {
	background-color:var(--GRN);
    border-color:var(--GRN);
}
body.nightmode .span.switchery.switchery-default.text-success {
	border-color:var(--RED);
	background-color:var(--RED);
}
body.nightmode .form-control {
    background-color:var(--10B) !important;
    border:1px solid var(--BRGBA25) !important;;
    color:#000;
}
body.nightmode .form-control:focus {
    background-color:var(--10B) !important;
    border:1px solid var(--HB) !important;
    -webkit-box-shadow:none;
    box-shadow:none;
    outline:0 !important;
    color:#000;
}
body.nightmode .form-control[disabled], .form-control[readonly], fieldset[disabled].form-control {
    background-color:rgba(0, 0, 0, .1);
    color:var(--10B) !important;
}
body.nightmode input.form-control::-webkit-input-placeholder {
    color:rgba(255, 255, 255, .3);
    font-weight:400;
}
body.nightmode input.form-control:-moz-placeholder {
    color:rgba(255, 255, 255, .3);
    font-weight:400;
}
body.nightmode input.form-control::-moz-placeholder {
    color:rgba(255, 255, 255, .3);
    font-weight:400;
}
body.nightmode input.form-control:-ms-input-placeholder {
    color:rgba(255, 255, 255, .3);
    font-weight:400;
}
body.nightmode .label {
	display:inline-block;
    padding:1px 5px !important;
	font-size:12px;
    font-weight:400 !important;
	line-height:1.5;
    color:var(--10B) !important;
	vertical-align:middle;
    border-radius:2px;
}
body.nightmode .label-default {
    background-color:var(--70B) !important;
	border:1px solid var(--70B)!important;
    margin-top: -7px !important; /* alignment fix */
    margin-right: 2px !important; /* alignment fix */
}
body.nightmode .label-primary {
    background-color:var(--HB) !important;
	border:1px solid var(--HB)!important;
}
body.nightmode .label-success {
    background-color:var(--GRN) !important;
	border:1px solid var(--GRN)!important;
}
body.nightmode .label-info {
    background-color:var(--HB) !important;
	border:1px solid var(--HB)!important;
}
body.nightmode .label-warning {
    background-color:var(--ORG) !important;
	border:1px solid var(--ORG)!important;
}
body.nightmode .label-danger {
    background-color:var(--RED) !important;
		border:1px solid var(--RED)!important;
}
body.nightmode .label-inverse {
    background-color:var(--HB)!important;
	border:1px solid var(--HB)!important;
}
body.nightmode .badge-sm, .badge-xs {
    -webkit-transform:translate(0, -2px);
    -ms-transform:translate(0, -2px);
    -o-transform:translate(0, -2px);
    transform:translate(0, -2px);
}
body.nightmode .badge-primary {
    background-color:var(--HB) !important;
}
body.nightmode .badge-success {
    background-color:var(--GRN) !important;
}
body.nightmode .badge-info {
    background-color:#3ddcf7;
}
body.nightmode .badge-warning {
    background-color:var(--ORG) !important;
}
body.nightmode .badge-danger {
    background-color:var(--RED) !important;
}
body.nightmode .badge-purple {
    background-color:var(--PUR) !important;
}
body.nightmode .badge-pink {
    background-color:var(--PIN) !important;
}
body.nightmode .badge-inverse {
    background-color:var(--HB);
}
body.nightmode .pagination>li>a, .pagination>li>span {
    color: var(--10B) !important;
    background-color:transparent;
    border:1px solid rgba(0, 0, 0, .1);
}
body.nightmode .pagination>li>a:focus, .pagination>li>a:hover, .pagination>li>span:focus, .pagination>li>span:hover {
	background-color:var(--HB) !important;
	color:var(--00B) !important;
	will-change:opacity, transform;
    -webkit-transition:all.3s ease-out;
    -moz-transition:all.3s ease-out;
    -o-transition:all.3s ease-out;
    -ms-transition:all.3s ease-out;
    transition:all.3s ease-out;
}
body.nightmode .pagination-split li a {
    -moz-border-radius:3px;
    -webkit-border-radius:3px;
    border-radius:3px;
}
body.nightmode .pagination>.active>a, .pagination>.active>a:focus, .pagination>.active>a:hover, .pagination>.active>span, .pagination>.active>span:focus, .pagination>.active>span:hover {
    background-color:var(--HB) !important;
    border-color:var(--HB) !important;
}
body.nightmode .pager li>a, .pager li>span {
    -moz-border-radius:3px;
    -webkit-border-radius:3px;
    border-radius:3px;
    color: var(--10B) !important;
    background:0 0;
}
body.nightmode .pager li>a:hover, .pager li>span:hover {
    background:rgba(255, 255, 255, .2);
}
body.nightmode .pager.disabled>a, .pager.disabled>a:focus, .pager.disabled>a:hover, .pager.disabled>span, .pagination>.disabled>a, .pagination>.disabled>a:focus, .pagination>.disabled>a:hover, .pagination>.disabled>span, .pagination>.disabled>span:focus, .pagination>.disabled>span:hover {
    background:rgba(255, 255, 255, .2);
    color: var(--10B) !important;
    border:1px solid rgba(0, 0, 0, .1);
}
body.nightmode blockquote.small, blockquote footer, blockquote small {
    color: var(--10B) !important;
}
body.nightmode .tabs li.tab a {
    -moz-transition:color.28s ease;
    -ms-transition:color.28s ease;
    -o-transition:color.28s ease;
    -webkit-transition:color.28s ease;
    color:#eee;
    transition:color.28s ease;
}
body.nightmode .tabs li.tab a:active {
    color:var(--HB) !important;
}
body.nightmode .tabs.indicator {
    background-color:var(--HB) !important;
}
body.nightmode .nav-pills li.active a, .nav-pills li.active a:focus, .nav-pills li.active a:hover {
    background-color:var(--HB) !important;
}
body.nightmode .nav-pills li a:hover {
    color:var(--00B) !important;
    background-color:var(--60B) !important;
}
body.nightmode .nav.nav-tabs + .tab-content {
    border:1px solid rgba(0, 0, 0, .1) !important;
	border-radius:0 3px 3px 3px !important;
    color:var(--10B) !important;
    background-color: var(--80B) !important;
}
body.nightmode .tabs-vertical-env.tab-content {
    border:1px solid rgba(0, 0, 0, .1);
    color:var(--10B) !important
    background-color: var(--80B) !important
}
body.nightmode .tabs-vertical-env.nav.tabs-vertical li.active>a {
    background-color:var(--10B) !important;
}
body.nightmode .tabs-vertical-env.nav.tabs-vertical li>a {
    color:#333
}
body.nightmode .nav.nav-tabs {
    border-bottom:0;
	-moz-transition:color.28s ease;
    -ms-transition:color.28s ease;
    -o-transition:color.28s ease;
    -webkit-transition:color.28s ease;
     transition:color.28s ease;
}
body.nightmode .nav.nav-tabs>li>a, body.nightmode .nav.tabs-vertical>li>a {
      background:var(--70B) !important;
      border:none !important;
	  border-radius:2px 2px 0 0 !important;
      margin:0 !important;
}
body.nightmode .nav.nav-tabs>li>a:hover, body.nightmode .nav.tabs-vertical>li>a:hover {
      color:var(--00B) !important;
      background:var(--60B) !important;
      border:none !important;
	  will-change:opacity, transform;
      -webkit-transition:all.3s ease-out;
      -moz-transition:all.3s ease-out;
      -o-transition:all.3s ease-out;
      -ms-transition:all.3s ease-out;
      transition:all.3s ease-out;
}
body.nightmode .navtab-custom li {
      background:var(--80B) !important;
      border:1px solid rgba(0, 0, 0, .1) !important;
      border-bottom:none !important;
      border-radius:3px 3px 0 0 !important;
      margin-bottom:-1px !important;
      margin-right:-1px !important;
}
body.nightmode .navtab-custom li a {
	background:var(--80B) !important;
    border-top:1px solid transparent !important;
}
body.nightmode .navtab-custom li.active a {
      background-color:var(--100B) !important;
      border:none !important;
}
body.nightmode .nav-tab-left.navtab-custom li a {
      background-color:var(--100B) !important;
      border:none !important;
}
body.nightmode .nav-tab-left.navtab-custom li.active a {
      background-color:var(--100B) !important;
      border:none !important;
}
body.nightmode .nav-tab-right.navtab-custom li a {
    border:none !important;
    border-right:1px solid transparent !important;
}
body.nightmode .nav-tab-right.navtab-custom li.active a {
    border-right:1px solid var(--HB) !important;
}
body.nightmode .nav-tabs>li.active>a, .nav-tabs>li.active>a:focus, .nav-tabs>li.active>a:hover, .tabs-vertical>li.active>a, .tabs-vertical>li.active>a:focus, .tabs-vertical>li.active>a:hover {
      color:var(--010B) !important;
      background:var(--80B) !important;
      border:none !important;
}
body.nightmode .swal2-popup {
	background-color:var(--BRGBA50) !important;
    border:1px solid var(--WRGBA25);
	backdrop-filter:blur(4px);
}
.swal2-popup .swal2-content {
    color:var(--10B) !important;
}
body.nightmode .swal2-popup .swal2-styled:focus {
    outline:0;
    -webkit-box-shadow:none;
    box-shadow:none;
}
body.nightmode .swal2-icon.swal2-warning {
    border-color:var(--ORG) !important;
	color:var(--ORG) !important;
}
body.nightmode .modal .modal-dialog {
    -moz-box-shadow:none;
    -webkit-box-shadow:none;
    border-color:rgba(238, 238, 238, .3);
    box-shadow:none;
    background:none !important;
}
body.nightmode .modal-content {
    background-color:var(--BRGBA50) !important;
    border:1px solid var(--WRGBA25);
	backdrop-filter:blur(4px);
}
body.nightmode .modal.modal-dialog.modal-content.modal-header {
    border-bottom:1px solid rgba(238, 238, 238, .3);
}
body.nightmode .modal.modal-dialog.modal-content.modal-footer {
    border-top:1px solid rgba(238, 238, 238, .3);
}
body.nightmode .modal.close {
    color:var(--10B) !important;
}
body.nightmode .modal-backdrop {
    background-color:#0F1215;
}
body.nightmode .modal-demo {
    background-color:var(--10B) !important;
}
body.nightmode .modal-demo.close {
    color:#eee;
}
body.nightmode .custom-modal-title {
    background-color:var(--HB) !important;
    color:var(--10B) !important;
}
body.nightmode .alert-success {
    background-color:var(--GRNRGBA25) !important;
    border-color:var(--GRNRGBA50) !important;
    color:var(--GRN) !important;
}
body.nightmode .alert-success.alert-link {
    color:var(--GRN) !important;
}
body.nightmode .alert-info {
    background-color:var(--HBRGBA25) !important;
    border-color:var(--HBRGBA50) !important;
    color:var(--HB) !important;
}
body.nightmode .alert-info.alert-link {
    color:var(--HB) !important;
}
body.nightmode .alert-warning {
    background-color:var(--ORGRGBA25) !important;
    border-color:var(--ORGRGBA25) !important;
    color:var(--ORG) !important;
}
body.nightmode .alert-warning.alert-link {
    color:var(--ORG) !important;
}
body.nightmode .alert-danger {
    background-color:var(--REDRGBA25) !important;
    border-color:var(--REDRGBA50) !important;
    color:var(--RED) !important;
}
body.nightmode .alert-danger.alert-link {
    color:var(--RED) !important;
}
body.nightmode .list-group-item {
    border:1px solid rgba(238, 238, 238, .3);
    background:0 0;
    color:var(--10B) !important;
}
body.nightmode .list-group-item.disabled, .list-group-item.disabled:focus, .list-group-item.disabled:hover, .list-group-item:hover {
    background-color:rgba(255, 255, 255, .07) !important:
}
body.nightmode .list-group-item.active, .list-group-item.active:focus, .list-group-item.active:hover {
    background-color:var(--HB) !important;
    border-color:var(--HB) !important;
}
body.nightmode .list-group-item.disabled.list-group-item-text, .list-group-item.disabled:focus.list-group-item-text, .list-group-item.disabled:hover.list-group-item-text {
    color:rgba(255, 255, 255, .5);
}
body.nightmode a.list-group-item.list-group-item-heading, button.list-group-item.list-group-item-heading {
    color:var(--10B) !important;
}
body.nightmode .nav-pills>.active>a>.badge {
    color:var(--HB) !important;
}
body.nightmode .has-success.form-control {
    border-color:var(--GRN) !important;
    box-shadow:none !important;
}
body.nightmode .has-warning.form-control {
    border-color:var(--ORG) !important;
    box-shadow:none !important;
}
body.nightmode .has-error.form-control {
    border-color:var(--RED) !important;
    box-shadow:none !important;
}
body.nightmode .input-group-addon {
    background-color:rgba(255, 255, 255, .2);
    border:2px solid rgba(238, 238, 238, .1);
    color:#EAEAEA;
}
body.nightmode .popover.popover-title {
    background-color:transparent;
    color:var(--HB) !important;
    font-weight:600;
}
body.nightmode .bx-shadow {
    -moz-box-shadow:0 1px 2px 0 rgba(0, 0, 0, .1);
    -webkit-box-shadow:0 1px 2px 0 rgba(0, 0, 0, .1);
    box-shadow:0 1px 2px 0 rgba(0, 0, 0, .1);
}
body.nightmode .grid-structure.grid-container {
    background-color:rgba(255, 255, 255, .03);
}
body.nightmode .icon-list-demo div {
    color:#98a6ad;
}
body.nightmode .icon-list-demo.col-md-4:hover {
    color:var(--HB) !important;
}
body.nightmode .waves-effect.waves-ripple {
    background:rgba(0, 0, 0, .2);
}
body.nightmode .waves-effect.waves-light.waves-ripple {
    background-color:rgba(255, 255, 255, .45);
}
body.nightmode .waves-effect.waves-red.waves-ripple {
    background-color:rgba(244, 67, 54, .7);
}
body.nightmode .waves-effect.waves-yellow.waves-ripple {
    background-color:rgba(255, 235, 59, .7);
}
body.nightmode .waves-effect.waves-orange.waves-ripple {
    background-color:rgba(255, 152, 0, .7);
}
body.nightmode .waves-effect.waves-purple.waves-ripple {
    background-color:rgba(156, 39, 176, .7);
}
body.nightmode .waves-effect.waves-green.waves-ripple {
    background-color:rgba(76, 175, 80, .7);
}
body.nightmode .waves-effect.waves-teal.waves-ripple {
    background-color:rgba(0, 150, 136, .7);
}
body.nightmode .waves-effect.waves-primary.waves-ripple {
    background-color:rgba(59, 175, 218, .4);
}
body.nightmode .page-title-box {
    background:var(--90B) !important;
    box-shadow:0 3px 3px 0px rgb(0 0 0/20%) !important;
    border:0 0 0 0 transparent;
}
body.nightmode .chzn-container-multi.chzn-choices {
    border:1px solid #aaa;
    background-color:#232368;
}
body.nightmode .daterangepicker.calendar-table {
    background:#232368;
    border:1px solid rgba(255, 255, 255, .07);
}
body.nightmode .daterangepicker td.off, .daterangepicker td.off.end-date, .daterangepicker td.off.in-range, .daterangepicker td.off.start-date {
    color:#999;
    background:#1C2127;
}
body.nightmode .daterangepicker td.in-range {
    color:#232368!important;
    background:#ebf4f8 !important;
}
body.nightmode#cj-wrapper.panel-default {
    border-color:rgba(255, 255, 255, .07);
}
body.nightmode#cj-wrapper.panel {
    margin-bottom:20px;
    background-color:var(--80B) !important;
    border:1px solid rgba(255, 255, 255, .07);
    border-radius:4px;
    -webkit-box-shadow:0 1px 1px rgba(0, 0, 0, .05);
    box-shadow:0 1px 1px rgba(0, 0, 0, .05);
}
body.nightmode#cj-wrapper.list-group-item {
    background-color:var(--80B) !important;
    border:1px solid rgba(255, 255, 255, .07);
}
body.nightmode#cj-wrapper.panel-footer {
    background-color:var(--90B) !important;
    border-top:1px solid transparent;
    border-radius:3px;
}
body.nightmode#cj-wrapper.panel-default >.panel-heading {
    color:rgba(255, 255, 255, .8);
    background-color:var(--80B) !important;
    border-color:transparent;
}
body.nightmode#cj-wrapper.thumbnail {
    background-color:#232368;
    border:1px solid rgba(255, 255, 255, .07);
}
body.nightmode .portlet.portlet-body {
    background:0 0;
}
body.nightmode .portlet .portlet-heading, body.nightmode .portlet .portlet-heading .portlet-title {
    color:var(--10B) !important;
}
body.nightmode .side-menu.left {
    background:var(--80B) !important;
    box-shadow:3px 0px 3px rgb(0 0 0/20%) !important;
    color:var(--10B) !important;
}
body.nightmode .side-menu.left a {
    color:var(--10B) !important;
}
body.nightmode .menu-title {
    color:var(--HB) !important;
}
body.nightmode .side-bar-right {
    background:var(--80B) !important;
    box-shadow: -3px 0px 3px rgb(0 0 0/20%) !important;
    color:var(--10B) !important;
}
.table>thead>tr>th, .table>tbody>tr>td, .table>tbody>tr>th, .table>tfoot>tr>td, .table>tfoot>tr>th, .table>thead>tr>td {
    border-top:1px solid rgba(0, 0, 0, .1);
}
.table>thead>tr>th {
    border-bottom:2px solid rgba(0, 0, 0, .1);
}
body.nightmode tbody {
    color:var(--10B) !important;
}
body.nightmode th {
    color:var(--10B) !important;
    font-size:15px;
    font-weight:500;
}
body.nightmode .table-hover>tbody>tr:
hover, .table-striped>tbody>tr:
nth-of-type(odd), .table>tbody>tr.active>td, .table>tbody>tr.active>th, .table>tbody>tr>td.active, .table>tbody>tr>th.active, .table>tfoot>tr.active>td, .table>tfoot>tr.active>th, .table>tfoot>tr>td.active, .table>tfoot>tr>th.active, .table>thead>tr.active>td, .table>thead>tr.active>th, .table>thead>tr>td.active, .table>thead>tr>th.active {
    background-color:var(--80B) !important;
}
body.nightmode .table>tbody>tr.success>td, .table>tbody>tr.success>th, .table>tbody>tr>td.success, .table>tbody>tr>th.success, .table>tfoot>tr.success>td, .table>tfoot>tr.success>th, .table>tfoot>tr>td.success, .table>tfoot>tr>th.success, .table>thead>tr.success>td, .table>thead>tr.success>th, .table>thead>tr>td.success, .table>thead>tr>th.success {
    background-color:rgba(0, 177, 157, .15);
}
body.nightmode .table>tbody>tr.info>td, .table>tbody>tr.info>th, .table>tbody>tr>td.info, .table>tbody>tr>th.info, .table>tfoot>tr.info>td, .table>tfoot>tr.info>th, .table>tfoot>tr>td.info, .table>tfoot>tr>th.info, .table>thead>tr.info>td, .table>thead>tr.info>th, .table>thead>tr>td.info, .table>thead>tr>th.info {
    background-color:rgba(61, 220, 247, .15);
}
body.nightmode .table>tbody>tr.warning>td, .table>tbody>tr.warning>th, .table>tbody>tr>td.warning, .table>tbody>tr>th.warning, .table>tfoot>tr.warning>td, .table>tfoot>tr.warning>th, .table>tfoot>tr>td.warning, .table>tfoot>tr>th.warning, .table>thead>tr.warning>td, .table>thead>tr.warning>th, .table>thead>tr>td.warning, .table>thead>tr>th.warning {
    background-color:rgba(255, 170, 0, .15);
}
body.nightmode .table>tbody>tr.danger>td, .table>tbody>tr.danger>th, .table>tbody>tr>td.danger, .table>tbody>tr>th.danger, .table>tfoot>tr.danger>td, .table>tfoot>tr.danger>th, .table>tfoot>tr>td.danger, .table>tfoot>tr>th.danger, .table>thead>tr.danger>td, .table>thead>tr.danger>th, .table>thead>tr>td.danger, .table>thead>tr>th.danger {
    background-color:rgba(239, 83, 80, .15);
}
.table-bordered {
    border:1px solid rgba(238, 238, 238, .3);
}
body.nightmode .table-striped>tbody>tr:nth-of-type(odd) {
    background-color:var(--80B) !important;
}
body.nightmode .table-bordered>tbody>tr>td, .table-bordered>tbody>tr>th, .table-bordered>tfoot>tr>td, .table-bordered>tfoot>tr>th, .table-bordered>thead>tr>td, .table-bordered>thead>tr>th {
    border:1px solid rgba(255, 255, 255, .2);
}
body.nightmode .table-hover>tbody>tr:hover, body.nightmode .table-striped>tbody>tr:nth-of-type(odd), body.nightmode .table>tbody>tr.active>td, body.nightmode .table>tbody>tr.active>th, body.nightmode .table>tbody>tr>td.active, body.nightmode .table>tbody>tr>th.active, body.nightmode .table>tfoot>tr.active>td, body.nightmode .table>tfoot>tr.active>th, body.nightmode .table>tfoot>tr>td.active, body.nightmode .table>tfoot>tr>th.active, body.nightmode .table>thead>tr.active>td, body.nightmode .table>thead>tr.active>th, body.nightmode .table>thead>tr>td.active, body.nightmode .table>thead>tr>th.active {
    background-color:var(--70B) !important;
}
body.nightmode .btn-default, body.nightmode .btn-default:active, body.nightmode .btn-default:focus, body.nightmode .btn-default:hover, body.nightmode .dropdown-toggle.btn-default {
    border-color:var(--HB) !important;
    background-color:transparent !important;
}
body.nightmode .btn-default:active, body.nightmode .btn-default:focus, body.nightmode .btn-default:hover, body.nightmode .dropdown-toggle.btn-default:hover {
    border-color:var(--HB) !important;
    background-color:var(--HB) !important;
}
body.nightmode .btn-group.open.dropdown-toggle {
    -webkit-box-shadow:0 0 0 100px rgba(0, 0, 0, .1)inset;
    box-shadow:0 0 0 100px rgba(0, 0, 0, .1)inset;
}
.btn {
	position:relative;
    cursor:pointer;
    display:inline-block;
    overflow:hidden;
    -webkit-user-select:none;
    -moz-user-select:none;
    -ms-user-select:none;
    user-select:none;
    -webkit-tap-highlight-color:transparent;
    vertical-align:middle;
    z-index:1;
    will-change:opacity,
    transform;
    -webkit-transition:all.3s ease-out;
    -moz-transition:all.3s ease-out;
    -o-transition:all.3s ease-out;
    -ms-transition:all.3s ease-out;
    transition:all.3s ease-out
}
body.nightmode .btn {
    color:var(--10B);
}
body.nightmode .btn-default {
    color:var(--10B) !important;
}
body.nightmode .btn-link {
    color:var(--10B);
}
body.nightmode .btn-link.pull-right {
    margin-right: -6px !important; /* alignment fix */
    padding-left: 18px !important; /* alignment fix */
}
.btn-link:focus, .btn-link:hover {
    color:var(--00B);
    text-decoration:none;
}
body.nightmode .btn-danger, .btn-info, .btn-inverse, .btn-pink, .btn-primary, .btn-purple, .btn-success, .btn-warning {
    color:var(--10B) !important;
}
body.nightmode .btn-bordered, .btn.btn-danger.btn-bordered, .btn.btn-info.btn-bordered, .btn.btn-primary.btn-bordered, .btn.btn-success.btn-bordered, .btn.btn-warning.btn-bordered, .btn.btn-inverse.btn-bordered {
    color:var(--10B) !important;
}
body.nightmode .btn-primary {
    background-color:transparent !important;
    border:1px solid var(--HB) !important;
}
body.nightmode .btn-primary.active, body.nightmode .btn-primary.focus, body.nightmode .btn-primary:active, body.nightmode .btn-primary:focus, body.nightmode .btn-primary:hover, body.nightmode .dropdown-toggle.btn-primary {
    background-color:var(--HB) !important;
    border:1px solid var(--HB) !important;
}
body.nightmode .btn-success {
    background-color: transparent !important;
    border:1px solid var(--HB) !important;
}
body.nightmode .btn-success.active, body.nightmode .btn-success.focus, body.nightmode .btn-success:active, body.nightmode .btn-success:focus, body.nightmode .btn-success:hover, body.nightmode .dropdown-toggle.btn-success {
    background-color:var(--HB) !important;
    border:1px solid var(--HB) !important;
}
body.nightmode .btn-info {
    background-color:transparent !important;
    border:1px solid var(--HB) !important;
}
body.nightmode .btn-info:active, body.nightmode .btn-info:focus, body.nightmode .btn-infoactive, body.nightmode .btn-info:focus, body.nightmode .btn-info:hover, body.nightmode .dropdown-toggle.btn-info {
    background-color:var(--HB) !important;
    border:1px solid var(--HB) !important;
}
body.nightmode .btn-warning {
    background-color:var(--80B) !important;
    border:1px solid var(--ORG) !important;
}
body.nightmode .btn-warning:active, body.nightmode .btn-warning:focus, body.nightmode .btn-warning:active, body.nightmode .btn-warning:focus, body.nightmode .btn-warning:hover, body.nightmode .dropdown-toggle.btn-warning {
    background-color:var(--HB) !important;
    border:1px solid var(--HB) !important;
}
#panic-button {
    background-color:var(--80B) !important; /* remove "!important" on server CSS for transition */
    border:1px solid var(--RED) !important;
}
body.nightmode .btn-danger {
    background-color:transparent !important;
    border:1px solid var(--RED) !important;
}
body.nightmode .btn-danger:active, body.nightmode .btn-danger:focus, body.nightmode .btn-danger:active, body.nightmode .btn-danger:focus, body.nightmode .btn-danger:hover, body.nightmode .dropdown-toggle.btn-danger {
    background-color:var(--RED) !important;
    border:1px solid var(--RED) !important;
}
body.nightmode .btn-inverse, body.nightmode .btn-inverse:active, body.nightmode .btn-inverse:focus, body.nightmode .btn-inverse:active, body.nightmode .btn-inverse:focus, body.nightmode .btn-inverse:hover, body.nightmode .dropdown-toggle.btn-inverse{
    background-color:var(--HB) !important;
    border:1px solid var(--HB) !important;
}
body.nightmode .btn-purple {
    background-color:var(--PUR) !important;
    border:1px solid var(--PUR) !important;
}
body.nightmode .btn-purple:active, body.nightmode .btn-purple:focus, body.nightmode .btn-purple:hover {
    background-color:#6254b2 !important;
    border:1px solid #6254b2 !important;
}
body.nightmode .btn-pink {
    background-color:var(--PIN) !important;
    border:1px solid var(--PIN) !important;
}
body.nightmode .btn-pink:active, body.nightmode .btn-pink:focus, body.nightmode .btn-pink:hover {
    background-color:#f64b87 !important;
    border:1px solid #f64b87 !important;
}
body.nightmode .btn-custom {
    border-bottom:3px solid transparent
}
body.nightmode .btn-custom.btn-default {
    background-color:#dae6ec;
    border-bottom:2px solid #a4b6bf !important;
}
body.nightmode .btn-custom.btn-primary {
    border-bottom:2px solid #2494be !important;
}
body.nightmode .btn-custom.btn-success {
    border-bottom:2px solid #007e70 !important;
}
body.nightmode .btn-custom.btn-info {
    border-bottom:2px solid #08aac6 !important;
}
body.nightmode .btn-custom.btn-warning {
    border-bottom:2px solid #c80 !important;
}
body.nightmode .btn-custom.btn-danger {
    border-bottom:2px solid #c71612 !important;
}
body.nightmode .btn-custom.btn-inverse {
    border-bottom:2px solid #21252c !important;
}
body.nightmode .btn-custom.btn-purple {
    border-bottom:2px solid #443a80 !important;
}
body.nightmode .btn-custom.btn-pink {
    border-bottom:2px solid #e80c59 !important;
}
body.nightmode .panel, body.nightmode .panel.panel-color.panel-primary {
    background-color:var(--BRGBA50) !important;
    border:1px solid var(--WRGBA25);
	backdrop-filter:blur(4px);
}
body.nightmode .panel.panel-body, body.nightmode .panel.panel-body, body.nightmode p-0 {
    color:var(--10B) !important;
	background:none !important;
}
body.nightmode .p-0 {
    color:var(--10B) !important;
	background:none !important;
}
body.nightmode .panel-default>.panel-heading {
    background-color:rgba(255, 255, 255, .2);
    border-bottom:none;
}
body.nightmode .panel-title {
    color:var(--10B) !important;
}
body.nightmode .m-t-10 {
    margin-top:10px !important;
    margin-bottom:10px !important;
}
body.nightmode .modal-dialog {
    width:768px;
    margin:30px auto;
}
body.nightmode .panel-sub-title {
    color:rgba(255, 255, 255, .6) !important;
}
body.nightmode .panel-footer {
    background:0 0;
    border-top:1px solid rgba(238, 238, 238, .2);
}
body.nightmode .panel-color.panel-title {
    color:var(--10B) !important;
}
body.nightmode .panel-primary>.panel-heading {
    background-color:var(--HB) !important;
}
body.nightmode .panel-info>.panel-heading, body.nightmode .panel-primary>.panel-heading, body.nightmode .panel-color.panel-info{
    background:none !important;
}
body.nightmode .panel-success>.panel-heading {
    background-color:var(--GRN) !important;
}
body.nightmode .panel-info>.panel-heading, body.nightmode .panel-primary>.panel-heading, body.nightmode panel-color.panel-info{
    background-color:var(--HB) !important;
}
body.nightmode .panel-info>.panel-primary {
    background:none !important;
}
body.nightmode .panel-warning>.panel-heading {
    background-color:var(--ORG) !important;
}
body.nightmode .panel-danger>.panel-heading {
    background-color:var(--RED) !important;
}
body.nightmode .panel-purple>.panel-heading {
    background-color:var(--PUR) !important;
}
body.nightmode .panel-pink>.panel-heading {
    background-color:var(--PIN) !important;
}
body.nightmode .panel-inverse>.panel-heading {
    background-color:var(--HB);
}
body.nightmode .panel-border {
    border-radius:3px;
}
body.nightmode .panel-border.panel-heading {
    background-color:transparent;
    border-top:3px solid #ccc !important;
    border-radius:3px;
    padding:10px 20px 0;
}
body.nightmode .panel-border.panel-primary.panel-heading {
    border-color:var(--HB) !important;
    color:var(--HB) !important;
}
body.nightmode .panel-border.panel-success.panel-heading {
    border-color:var(--GRN) !important;
    color:var(--GRN) !important;
}
body.nightmode .panel-border.panel-info.panel-heading {
    border-color:var(--HB) !important;
    color:var(--HB) !important;
}
body.nightmode .panel-border.panel-warning.panel-heading {
    border-color:var(--ORG) !important;
    color:var(--ORG) !important;
}
body.nightmode .panel-border.panel-danger.panel-heading {
    border-color:var(--RED) !important;
    color:var(--RED) !important;
}
body.nightmode .panel-border.panel-purple.panel-heading {
    border-color:var(--PUR) !important;
    color:var(--PUR) !important;
}
body.nightmode .panel-border.panel-pink.panel-heading {
    border-color:var(--PIN)!important;
    color:var(--PIN) !important;
}
body.nightmode .panel-border.panel-inverse.panel-heading {
    border-color:var(--HB) !important;
    color:var(--HB) !important;
}
body.nightmode .panel-group.panel-group-joined.panel + .panel {
    border-top:1px solid rgba(255, 255, 255, .3);
}
body.nightmode .panel-group-joined.panel-group.panel + .panel {
    border-top:1px solid #eee;
}
body.nightmode .portlet, .card-box {
	border:none !important;
    background-color:var(--80B) !important;
    -moz-border-radius:3px !important;
    -webkit-border-radius:3px !important;
    border-radius:3px !important;
	box-shadow:0 3px 3px 0px rgb(0 0 0/20%) !important;
}
body.nightmode .portlet .portlet-heading, body.nightmode, .portlet-title {
    color:var(--10B) !important;
}
body.nightmode .portlet, .portlet-body, .body.nightmode, .portlet-heading a {
    color:var(--10B) !important;
}
body.nightmode .portlet, .portlet-heading, .bg-danger a, .bg-info a, .bg-inverse a, .bg-pink a, .bg-primary a, .bg-purple a, .bg-success a, .bg-warning a {
    color:var(--10B) !important;
}
body.nightmode .panel-disabled {
    background:rgba(238, 238, 238, .2);
}
body.nightmode .loader-1 {
    background-color:var(--HB) !important;
}
body.nightmode .checkbox label::before {
    background-color:transparent;
    border:1px solid #98a6ad;
}
body.nightmode .checkbox label::after {
    color:#eee;
}
body.nightmode .checkbox-danger input[type = checkbox]:
checked + label::after, .checkbox-info input[type = checkbox]:
checked + label::after, .checkbox-inverse input[type = checkbox]:checked + label::after, .checkbox-pink input[type = checkbox]:checked + label::after, .checkbox-primary input[type = checkbox]:checked + label::after, .checkbox-purple input[type = checkbox]:checked + label::after, .checkbox-success input[type = checkbox]:checked + label::after, .checkbox-warning input[type = checkbox]:checked + label::after {
    color:var(--10B) !important;
}
body.nightmode .checkbox input[type = checkbox]:disabled + label::before {
    background-color:#eee;
}
body.nightmode .checkbox-primary input[type = checkbox]:checked + label::before {
    background-color:var(--HB) !important;
    border-color:var(--HB) !important;
}
body.nightmode .checkbox-danger input[type = checkbox]:checked + label::before {
    background-color:var(--RED) !important;
    border-color:var(--RED) !important;
}
body.nightmode .checkbox-info input[type = checkbox]:checked + label::before {
    background-color:#3ddcf7;
    border-color:#3ddcf7;
}
body.nightmode .checkbox-warning input[type = checkbox]:checked + label::before {
    background-color:var(--ORG) !important;
    border-color:var(--ORG) !important;
}
body.nightmode .checkbox-success input[type = checkbox]:checked + label::before {
    background-color:var(--GRN) !important;
    border-color:var(--GRN) !important;
}
body.nightmode .checkbox-purple input[type = checkbox]:checked + label::before {
    background-color:var(--PUR) !important;
    border-color:var(--PUR) !important;
}
body.nightmode .checkbox-pink input[type = checkbox]:checked + label::before {
    background-color:var(--PIN) !important;
    border-color:var(--PIN) !important;
}
body.nightmode .checkbox-inverse input[type = checkbox]:checked + label::before {
    background-color:var(--HB) !important;
    border-color:var(--HB) !important;
}
body.nightmode .radio label::before {
    background-color:transparent;
    border:2px solid #98a6ad;
}
body.nightmode .radio label::after {
    background-color:#98a6ad;
}
body.nightmode .radio-primary input[type = radio] + label::after, .radio-primary input[type = radio]:checked + label::after {
    background-color:var(--HB) !important;
}
body.nightmode .radio input[type = radio]:disabled + label {
    opacity:.65;
}
body.nightmode .radio-primary input[type = radio]:checked + label::before {
    border-color:var(--HB) !important;
}
body.nightmode .radio-danger input[type = radio] + label::after, .radio-danger input[type = radio]:checked + label::after {
    background-color:var(--RED) !important;
}
body.nightmode .radio-danger input[type = radio]:checked + label::before {
    border-color:var(--RED) !important;
}
body.nightmode .radio-info input[type = radio] + label::after, .radio-info input[type = radio]:checked + label::after {
    background-color:#3ddcf7;
}
body.nightmode .radio-info input[type = radio]:checked + label::before {
    border-color:#3ddcf7;
}
body.nightmode .radio-warning input[type = radio] + label::after, .radio-warning input[type = radio]:checked + label::after {
    background-color:var(--ORG) !important;
}
body.nightmode .radio-warning input[type = radio]:checked + label::before {
    border-color:var(--ORG) !important;
}
body.nightmode .radio-success input[type = radio] + label::after, .radio-success input[type = radio]:checked + label::after {
    background-color:var(--GRN) !important;
}
body.nightmode .radio-success input[type = radio]:checked + label::before {
    border-color:var(--GRN) !important;
}
body.nightmode .radio-purple input[type = radio] + label::after, .radio-purple input[type = radio]:checked + label::after {
    background-color:var(--PUR) !important;
}
body.nightmode .radio-purple input[type = radio]:checked + label::before {
    border-color:var(--PUR) !important;
}
body.nightmode .radio-pink input[type = radio] + label::after, .radio-pink input[type = radio]:checked + label::after {
    background-color:var(--PIN) !important;
}
body.nightmode .radio-pink input[type = radio]:checked + label::before {
    border-color:var(--PIN) !important;
}
body.nightmode .radio-inverse input[type = radio] + label::after, .radio-inverse input[type = radio]:checked + label::after {
    background-color:var(--HB);
}
body.nightmode .radio-inverse input[type = radio]:checked + label::before {
    border-color:var(--HB);
}
body.nightmode .progress {
    -webkit-box-shadow:none !important;
    background-color:rgba(152, 166, 173, .4);
    box-shadow:none !important;
}
body.nightmode .ms-container.ms-list.ms-focus, .progress-bar {
    box-shadow:none;
}
body.nightmode .progress-bar-primary {
    background-color:var(--HB) !important;
}
body.nightmode .progress-bar-success {
    background-color:var(--GRN) !important;
}
body.nightmode .progress-bar-info {
    background-color:#3ddcf7;
}
body.nightmode .progress-bar-warning {
    background-color:var(--ORG) !important;
}
body.nightmode .progress-bar-danger {
    background-color:var(--RED) !important;
}
body.nightmode .progress-bar-inverse {
    background-color:var(--HB);
}
body.nightmode .progress-bar-purple {
    background-color:var(--PUR) !important;
}
body.nightmode .progress-bar-pink {
    background-color:var(--PIN) !important;
}
body.nightmode .modal-block {
    background:0 0;
}
body.nightmode#datatable-editable.form-control {
    background-color:transparent;
}
body.nightmode#datatable-editable.fa-times, body.nightmode#datatable-editable.fa-trash-o {
    color:var(--RED) !important;
}
body.nightmode#datatable-editable.fa-pencil {
    color:#29b6f6;
}
body.nightmode#datatable-editable.fa-save {
    color:#33b86c;
}
body.nightmode table.dataTable td.focus, table.dataTable th.focus {
    outline:var(--HB) solid 3px !important;
    outline-offset:-1px;
}
body.nightmode table.dataTable.dtr-inline.collapsed>tbody>tr>td:first-child:before, table.dataTable.dtr-inline.collapsed>tbody>tr>th:first-child:before {
    top:9px;
    left:6px;
    height:18px;
    width:18px;
	color:var(--10B);
	font-family:source sans pro,sans-serif!important;
	font-weight:700;
	text-indent:6px;
    line-height:17px;
    border:none;
	border-radius:3px;
    background-color:var(--HB);
	box-shadow:none;
}
body.nightmode table.dataTable.dtr-inline.collapsed>tbody>tr.parent>td:first-child:before, table.dataTable.dtr-inline.collapsed>tbody>tr.parent>th:first-child:before {
    background-color:var(--RED);
}
body.nightmode .fixedHeader-floating {
    border:none !important;
}
body.nightmode .fixedHeader-floating.sorting, .fixedHeader-floating.sorting_asc {
    background-color:var(--80B) !important;
    border-color:rgba(238, 238, 238, .3);
}
body.nightmode div.DTS tbody tr.even {
    background-color:#272e35;
}
body.nightmode div.DTS div.dataTables_scrollBody {
    background:0 0 !important;
}
body.nightmode .table-responsive {
    overflow:hidden
}
body.nightmode .table-rep-plugin.table-responsive {
    border:none !important;
}
body.nightmode .table-rep-plugin.dropdown-menu li.checkbox-row {
    color:var(--10B) !important;
    background-color:transparent!important
}
body.nightmode .table-rep-plugin.checkbox-row label::before {
    background-color: var(--10B) !important;
    border:1px solid #ccc;
}
body.nightmode .table-rep-plugin.checkbox-row label::after {
    color:#555
}
body.nightmode .table-rep-plugin.checkbox-row input[type = checkbox]:disabled + label::before {
    background-color:#eee;
}
body.nightmode .table-rep-plugin.checkbox-row input[type = checkbox]:checked + label::before {
    background-color:var(--HB) !important;
    border-color:var(--HB) !important;
}
body.nightmode .table-rep-plugin.checkbox-row input[type = checkbox]:checked + label::after {
    color:var(--10B) !important;
}
body.nightmode .footable-odd {
    background-color:#2e363e;
}
body.nightmode table.focus-on tbody tr.unfocused td, table.focus-on tbody tr.unfocused th {
    color:rgba(255, 255, 255, .25);
}
body.nightmode table.focus-on tbody tr.focused td, table.focus-on tbody tr.focused th {
    background-color:var(--HB) !important;
    color:var(--10B) !important;
}
body.nightmode .table-rep-plugin.sticky-table-header.fixed-solution {
    background-color:#272e35;
}
body.nightmode .error {
    color:var(--RED) !important;
}
body.nightmode .parsley-error {
    border-color:var(--RED) !important;
}
body.nightmode .parsley-errors-list>li {
    color:#f6504d;
}
body.nightmode .datepicker table tr td span.active, .datepicker table tr td span.active.disabled, .datepicker table tr td span.active.disabled:hover, .datepicker table tr td span.active:hover, .datepicker table tr td.selected, .datepicker table tr td.selected.disabled, .datepicker table tr td.selected.disabled:hover, .datepicker table tr td.selected:hover, .datepicker table tr td.today, .datepicker table tr td.today.disabled, .datepicker table tr td.today.disabled:hover, .datepicker table tr td.today:hover {
    background-image:none;
}
body.nightmode .datepicker table tr td span.active.active, .datepicker table tr td span.active.disabled, .datepicker table tr td span.active.disabled.active, .datepicker table tr td span.active.disabled.disabled, .datepicker table tr td span.active.disabled:active, .datepicker table tr td span.active.disabled:hover, .datepicker table tr td span.active.disabled:hover.active, .datepicker table tr td span.active.disabled:hover.disabled, .datepicker table tr td span.active.disabled:hover:active, .datepicker table tr td span.active.disabled:hover:hover, .datepicker table tr td span.active.disabled:hover[disabled], .datepicker table tr td span.active.disabled[disabled], .datepicker table tr td span.active:active, .datepicker table tr td span.active:hover, .datepicker table tr td span.active:hover.active, .datepicker table tr td span.active:hover.disabled, .datepicker table tr td span.active:hover:active, .datepicker table tr td span.active:hover:hover, .datepicker table tr td span.active:hover[disabled], .datepicker table tr td span.active[disabled]{
    background-color:var(--HB) !important;
}
body.nightmode .datepicker tfoot tr th:hover, .datepicker thead tr:first-child th:hover {
    background-color:#1c2127;
}
body.nightmode .datepicker-inline {
    border:2px solid rgba(238, 238, 238, .3);
}
body.nightmode .daterangepicker td.active, .daterangepicker td.active:hover {
    background-color:var(--HB) !important;
    border-color:var(--HB) !important;
}
body.nightmode .daterangepicker.input-mini.active {
    border:1px solid #AAA;
}
body.nightmode .daterangepicker.ranges li {
    background-clip:padding-box;
    color:#98a6ad;
    border-color:var(--80B) !important;
    background-color:var(--80B) !important;
}
body.nightmode .daterangepicker select.ampmselect, .daterangepicker select.hourselect, .daterangepicker select.minuteselect, .daterangepicker select.secondselect {
    border:1px solid #e3e3e3;
}
body.nightmode .daterangepicker.ranges li.active, .daterangepicker.ranges li:hover {
    background-color:var(--HB) !important;
    border:1px solid var(--HB) !important;
}
body.nightmode .ms-container.ms-selectable li.ms-elem-selectable, .ms-container.ms-selection li.ms-elem-selection {
    border-bottom:1px solid #2C343C;
}
body.nightmode .ms-container.ms-selectable li.ms-hover, .ms-container.ms-selection li.ms-hover {
    background-color:var(--HB) !important;
}
.active ms-hover {
    background-color:var(--10B) !important;
}
body.nightmode .note-editor {
    border:2px solid rgba(255, 255, 255, .2);
    position:relative;
    color:#98a6ad;
}
body.nightmode .note-editor.note-toolbar {
    background-color:transparent;
    border-bottom:1px solid #eee;
    margin:0;
}
body.nightmode .note-editor.note-statusbar {
    background-color:transparent;
}
body.nightmode .note-editor.note-editing-area.note-editable {
    background:0 0;
    color:#98a6ad;
}
body.nightmode .note-popover.popover.popover-content.note-color.dropdown-menu.btn-group.note-color-reset, .note-popover.popover.popover-content.note-color.dropdown-menu.btn-group.note-palette-title, .panel-heading.note-toolbar.note-color.dropdown-menu.btn-group.note-color-reset, .panel-heading.note-toolbar.note-color.dropdown-menu.btn-group.note-palette-title {
    color:var(--80B) !important;
}
body.nightmode .bootstrap-timepicker-widget table td a:hover {
    background-color:transparent;
    border-color:transparent;
    border-radius:4px;
    color:var(--HB) !important;
    text-decoration:none;
}
body.nightmode .datepicker table tr td.active, .datepicker table tr td.active.disabled, .datepicker table tr td.active.disabled:hover, .datepicker table tr td.active:hover {
    text-shadow:none;
    background-color:var(--HB) !important;
    background-image:none;
    box-shadow:none;
}
body.nightmode .fc-day {
    background:0 0;
}
body.nightmode .fc-widget-content, .fc-widget-header {
    border:1px solid #f5f5f5;
}
body.nightmode .fc th.fc-widget-header {
    background:rgba(255, 255, 255, .2);
    font-size:14px;
    line-height:20px;
    padding:10px 0;
    text-transform:uppercase;
}
body.nightmode .fc-unthemed.fc-divider, .fc-unthemed.fc-popover, .fc-unthemed.fc-row, .fc-unthemed tbody, .fc-unthemed td, .fc-unthemed th, .fc-unthemed thead {
    background-color:transparent;
    border-color:rgba(0, 0, 0, .1);
}
body.nightmode .fc-button {
    background:var(--10B) !important;
    border:1px solid #f5f5f5;
    color:#555;
    text-transform:capitalize;
}
body.nightmode .fc-state-hover {
    background:#F5F5F5;
}
body.nightmode .fc-cell-overlay, .fc-state-highlight {
    background:#f0f0f0;
}
body.nightmode .fc-unthemed.fc-today {
    background:0 0;
}
body.nightmode .external-event {
    color:var(--10B) !important;
    cursor:move;
    margin:10px 0;
    padding:6px 10px;
}
body.nightmode #chart_iframe_basechart {
    border:none !important;
    border-radius:3px !important;
    -moz-border-radius:3px !important;
    -webkit-border-radius:3px !important;
	box-shadow:0 3px 3px 0px rgb(0 0 0/20%) !important;
}
body.nightmode .tradingview-widget-container {
	display:flex;
	min-height:402px;
	border:none !important;
    background-color:var(--80B) !important;
    -moz-border-radius:3px !important;
    -webkit-border-radius:3px !important;
    border-radius:3px !important;
	box-shadow:0 3px 3px 0px rgb(0 0 0/20%) !important;
}
body.nightmode .tradingview-widget-copyright {
	display:none;
}
body.nightmode .inbox-widget.inbox-item {
    border-bottom:1px solid var(--80B) !important;
}
body.nightmode .inbox-widget.inbox-item.inbox-item-author {
    color:#f5f5f5;
    display:block;
    margin:0;
}
body.nightmode .conversation-list.chat-avatar i, .inbox-widget.inbox-item.inbox-item-date, .inbox-widget.inbox-item.inbox-item-text {
    color:var(--10B) !important;
}
body.nightmode .conversation-list.ctext-wrap {
    -moz-border-radius:3px;
    -webkit-border-radius:3px;
    background:rgba(0, 0, 0, .1);
    border-radius:3px;
    box-shadow:0 1px 2px rgba(0, 0, 0, .1);
}
body.nightmode .conversation-list.ctext-wrap i {
    color:#f5f5f5;
}
body.nightmode .conversation-list.ctext-wrap p {
    color:#98a6ad;
}
body.nightmode .conversation-list.ctext-wrap:after {
    border:solid transparent;
    border-top-color:rgba(0, 0, 0, .1);
    border-right-color:rgba(0, 0, 0, .1);
}
body.nightmode .conversation-list.odd.ctext-wrap:after {
    border-color:rgba(238, 238, 242, 0) !important;
    border-left-color:rgba(0, 0, 0, .1) !important;
    border-top-color:rgba(0, 0, 0, .1) !important;
}
body.nightmode .widget-panel i {
    background:rgba(255, 255, 255, .2);
}
body.nightmode .ms-container.ms-selectable, .ms-container.ms-selection {
    background:0 0;
    color:#98a6ad;
}
body.nightmode .sweet-alert h2 {
    color:var(--80B) !important;
}
body.nightmode .sweet-alert.icon.success.placeholder {
    border:4px solid rgba(0, 177, 157, .3);
}
body.nightmode .sweet-alert.icon.success.line {
    background-color:var(--GRN) !important;
}
body.nightmode .sweet-alert.icon.warning {
    border-color:var(--ORG) !important;
}
body.nightmode .sweet-alert.icon.info {
    border-color:#3ddcf7;
}
body.nightmode .sweet-alert.btn-cancel {
	background:transparent;
	border:1px solid var(--HB) !important;
}
body.nightmode .sweet-alert.btn-cancel:hover {
	background:var(--HB);
}
body.nightmode .sweet-alert.btn-danger:focus, .sweet-alert.btn-default:focus, .sweet-alert.btn-info:focus, .sweet-alert.btn-success:focus, .sweet-alert.btn-warning:focus {
    box-shadow:none;
}
body.nightmode .notifyjs-metro-base {
    color:#444;
    border-radius:3px;
    -webkit-border-radius:3px;
    box-shadow:0 1px 0 rgba(0, 0, 0, .2);
    -webkit-animation:dropdownOpen.3s ease-out;
    -o-animation:dropdownOpen.3s ease-out;
    animation:dropdownOpen.3s ease-out
}
body.nightmode .notifyjs-metro-cool {
    color:#fafafa !important;
    background-color:#4A525F;
    border:1px solid #4A525F;
}
body.nightmode .bootstrap-tagsinput {
    padding:3px 7px 6px;
    border:2px solid rgba(238, 238, 238, .3);
}
body.nightmode .bootstrap-tagsinput.label-info {
    background-color:var(--HB) !important;
}
body.nightmode .ms-container {
    background:url(../images/multiple-arrow.png)50% 50% no-repeat
}
body.nightmode .ms-container.ms-list {
    border:2px solid rgba(255, 255, 255, .2);
}
body.nightmode .ms-container.ms-list.ms-focus {
    border:2px solid rgba(255, 255, 255, .3);
}
body.nightmode .ms-selectable {
    outline:0 !important;
    box-shadow:none;
}
body.nightmode .ms-container.ms-selectable li.ms-hover, .ms-container.ms-selection li.ms-hover {
    color:var(--10B) !important;
}
body.nightmode .ms-container.ms-selectable, .ms-container.ms-selection {
    background-color:transparent;
}
body.nightmode .ms-container.ms-selectable li.ms-elem-selectable, .ms-container.ms-selection li.ms-elem-selection {
    color:#98a6ad;
}
body.nightmode .select2-container.select2-choice {
    background-image:none!important;
    border:none!important;
    background-color:transparent!important;
    box-shadow:none!important;
    color:#000;
}
body.nightmode .select2-container.select2-choice.select2-arrow {
    background-image:none !important;
    background:0 0;
}
body.nightmode .select2-results.select2-highlighted {
    color:var(--10B) !important;
    background-color:var(--HB) !important;
}
body.nightmode .select2-drop-active {
    border:1px solid #e3e3e3 !important;
    -webkit-box-shadow:0 2px 2px rgba(0, 0, 0, .15);
    box-shadow:0 2px 2px rgba(0, 0, 0, .15);
    -moz-box-shadow:0 2px 2px rgba(0, 0, 0, .15);
}
body.nightmode .select2-search input {
    border:1px solid #e3e3e3;
}
body.nightmode .select2-container-multi.select2-choices {
    border:2px solid rgba(255, 255, 255, .2) !important;
    box-shadow:none !important;
    background:0 0 !important;
    -webkit-border-radius:4px !important;
    border-radius:4px !important;
    -moz-border-radius:4px !important;
    background-clip:padding-box !important;
}
body.nightmode .select2-container-multi.select2-choices.select2-search-choice {
    color:var(--10B) !important;
    background:rgba(255, 255, 255, .2);
}
body.nightmode .bootstrap-timepicker-widget table td input {
    background-color:transparent;
}
body.nightmode .bootstrap-timepicker-widget table td a {
    color:rgba(238, 238, 238, .2);
}
body.nightmode .morris-hover.morris-default -style {
    background-color:#f5f5f5;
    color:var(--80B) !important;
}
body.nightmode .morris-hover.morris-default -style.morris-hover-point {
    color:var(--80B) !important;
}
body.nightmode .percent {
    color:#797979;
}
body.nightmode#flotTip {
    background-color:#f5f5f5;
    border:1px solid rgba(50, 59, 68, .1);
    color:var(--80B) !important;
    -webkit-border-radius:3px;
    -moz-border-radius:3px;
    border-radius:3px;
}
body.nightmode .legend div:
first-of-type {
    background-color:transparent !important;
}
body.nightmode .flot-tick-label {
    color:var(--10B) !important;
}
body.nightmode .ct-grid {
    stroke:rgba(0, 0, 0, .1);
}
body.nightmode .ct-chart.ct-label {
    fill:#a3afb7;
    color:#a3afb7;
}
body.nightmode .ct-chart.simple-pie-chart-chartist.ct-label {
    color:var(--10B) !important;
    fill:var(--10B) !important;
}
body.nightmode .ct-chart.ct-series.ct-series-a.ct-bar, .ct-chart.ct-series.ct-series-a.ct-line, .ct-chart.ct-series.ct-series-a.ct-point, .ct-chart.ct-series.ct-series-a.ct-slice-donut {
    stroke:var(--HB) !important;
}
body.nightmode .ct-chart.ct-series.ct-series-b.ct-bar, .ct-chart.ct-series.ct-series-b.ct-line, .ct-chart.ct-series.ct-series-b.ct-point, .ct-chart.ct-series.ct-series-b.ct-slice-donut {
    stroke:var(--PIN) !important;
}
body.nightmode .ct-chart.ct-series.ct-series-c.ct-bar, .ct-chart.ct-series.ct-series-c.ct-line, .ct-chart.ct-series.ct-series-c.ct-point, .ct-chart.ct-series.ct-series-c.ct-slice-donut {
    stroke:var(--GRN) !important;
}
body.nightmode .ct-chart.ct-series.ct-series-d.ct-bar, .ct-chart.ct-series.ct-series-d.ct-line, .ct-chart.ct-series.ct-series-d.ct-point, .ct-chart.ct-series.ct-series-d.ct-slice-donut {
    stroke:#3ddcf7;
}
body.nightmode .ct-chart.ct-series.ct-series-e.ct-bar, .ct-chart.ct-series.ct-series-e.ct-line, .ct-chart.ct-series.ct-series-e.ct-point, .ct-chart.ct-series.ct-series-e.ct-slice-donut {
    stroke:#797979;
}
body.nightmode .ct-chart.ct-series.ct-series-f.ct-bar, .ct-chart.ct-series.ct-series-f.ct-line, .ct-chart.ct-series.ct-series-f.ct-point, .ct-chart.ct-series.ct-series-f.ct-slice-donut {
    stroke:var(--PUR) !important;
}
body.nightmode .ct-chart.ct-series.ct-series-g.ct-bar, .ct-chart.ct-series.ct-series-g.ct-line, .ct-chart.ct-series.ct-series-g.ct-point, .ct-chart.ct-series.ct-series-g.ct-slice-donut {
    stroke:var(--ORG) !important;
}
body.nightmode .ct-series-a.ct-area, .ct-series-a.ct-slice-pie {
    fill:var(--HB) !important;
}
body.nightmode .ct-series-b.ct-area, .ct-series-b.ct-slice-pie {
    fill:var(--PIN) !important;
}
body.nightmode .ct-series-c.ct-area, .ct-series-c.ct-slice-pie {
    fill:var(--GRN) !important;
}
body.nightmode .ct-series-d.ct-area, .ct-series-d.ct-slice-pie {
    fill:#3ddcf7;
}
body.nightmode .jqstooltip {
    background-color:#36404a !important;
    border-color:#36404a !important;
}
body.nightmode .nvd3 text {
    fill:#98a6ad;
}
body.nightmode .nvd3.nv-axis line, .nvd3.nv-axis path {
    stroke:#2c333b;
}
body.nightmode .nvd3.nv-discretebar.nv-groups text, .nvd3.nv-multibarHorizontal.nv-groups text {
    fill:rgba(255, 255, 255, .8);
}
body.nightmode .multi-chart.nv-legend-symbol {
    fill:var(--10B) !important;
    fill-opacity:0;
    stroke:var(--10B) !important;
}
body.nightmode .portfolioFilter a {
    -moz-box-shadow:0 1px 2px 0 rgba(0, 0, 0, .1);
    -moz-transition:all.3s ease-out;
    -ms-transition:all.3s ease-out;
    -o-transition:all.3s ease-out;
    -webkit-box-shadow:0 1px 2px 0 rgba(0, 0, 0, .1);
    -webkit-transition:all.3s ease-out;
    box-shadow:0 1px 2px 0 rgba(0, 0, 0, .1);
    color:#98a6ad;
    padding:5px 10px;
    display:inline-block;
    transition:all.3s ease-out;
	color:var(--10B) !important;
}
body.nightmode portfolioFilter a:hover {
    background-color:var(--HB) !important;
		color:var(--00B) !important;
}
body.nightmode .thumb {
    background-color:var(--70B) !important;
    border-radius:3px;
    box-shadow:0 1px 1px 0 rgba(0, 0, 0, .1);
    border-color:transparent;
    margin-top:30px;
    width:100% ;
    padding:10px;
}
body.nightmode .gal-detail.ga-border {
    height:3px;
    width:40px;
    background-color:var(--HB) !important;
    margin:10px auto;
}
body.nightmode .pricing-column.plan-title {
    color:var(--GRN) !important;
}
body.nightmode .pricing-column.plan-price {
    color:var(--10B) !important;
}
body.nightmode .pricing-column.plan-duration {
    color:#98a6ad;
}
body.nightmode .ribbon span {
    color:var(--10B) !important;
    box-shadow:0 0 8px 0 rgba(0, 0, 0, .06),
    0 1px 0 0 rgba(0, 0, 0, .02);
    background:var(--GRN) !important;
    background:linear-gradient(var(--GRN) 0, var(--GRN) 100% ) !important;
}
body.nightmode .bg-muted, .white-well {
    background-color:#232368 !important;
}
body.nightmode .ribbon span:before {
    border-left:3px solid #007e70;
    border-right:3px solid transparent;
    border-bottom:3px solid transparent;
    border-top:3px solid #007e70;
}
body.nightmode .ribbon span:after {
    border-left:3px solid transparent;
    border-right:3px solid #007e70;
    border-bottom:3px solid transparent;
    border-top:3px solid #007e70;
}
body.nightmode .nav.nav-tabs>li.active>a, .nav.nav-tabs>li>a {
    color:var(--10B) !important;
}
body.nightmode .page-title-box {
     background:var(--90B) !important;
}
body.nightmode .content-page.page-title-box.btn-link {
    color:#98a6ad !important;
}
body.nightmode .white-well {
    box-shadow:none;
    border:1px solid #424A51;
}
body.nightmode .pricing-num {
    border:12px solid var(--80B) !important;
}
body.nightmode .card-box .nav-pills li a {
    color:var(--10B) !important; /* remove "!important" on server CSS for transition */
	background-color:var(--70B);
}
body.nightmode .card-box .nav-pills li.active a {
    color:var(--10B) !important;
}
body.nightmode .card-box .nav-pills li a.groupHasError, .groupHasError {
    color:var(--RED) !important;
}
body.nightmode .card-box .nav-pills li.active a.groupHasError {
    background-color:var(--RED) !important;
    color:var(--10B) !important;
}
body.nightmode#xiWindowBody.upgrade-options select option {
    color:#8D8D8D;
}
body.nightmode#xiWindowBody.upgrade-options select {
    color:#000;
}
body.nightmode .tab-content {
    color:var(--10B) !important;
	box-shadow:0 3px 3px 0px rgb(0 0 0/20%) !important;
}
body.nightmode .help-block {
    color:var(--10B) !important;
}
body.nightmode .exchange_logo_img {
    background-color:var(--10B) !important;
    -webkit-border-radius:5px;
    -moz-border-radius:5px;
    border-radius:5px;
    rgba(238, 238, 238, .1);
    padding-left:15px;
    padding-right:15px;
}
body.nightmode .color-navy, .page-title-box.page-title {
    color:var(--10B) !important;
}
body.nightmode .color-navy, .editable-click, .page-title-box.page-title, a.editable-click, a.editable-click:hover, h3.hopperBoxTitle {
    color:var(--10B) !important;
}
body.nightmode .modal-demo.btn, .modal-demo h3, .modal-demo h4, .modal-demo h4 a, .modal-demo p {
    color:#232368;
}
body.nightmode .calendar.daterangepicker_input.calendar-time select, .calendar.daterangepicker_input.fa {
    color:#1c2127;
}
body.nightmode .calendar.calendar-table td.available:hover {
    color:#1c2127 !important;
}
body.nightmode#discount-modal p {
    color:var(--HB);
}
body.nightmode#discount-modal.form-control {
    color:rgba(0, 0, 0, .6);
}
body.nightmode#discount-modal input.form-control::placeholder {
    color:rgba(0, 0, 0, .3) !important;
}
body.nightmode#discount-modal input.form-control::-webkit-input-placeholder {
    color:rgba(0, 0, 0, .3) !important;
}
body.nightmode#discount-modal input.form-control:-moz-placeholder {
    color:rgba(0, 0, 0, .3) !important;
}
body.nightmode#discount-modal input.form-control::-moz-placeholder {
    color:rgba(0, 0, 0, .3) !important;
}
body.nightmode#discount-modal input.form-control:-ms-input-placeholder {
    color:rgba(0, 0, 0, .3) !important;
}
body.nightmode#discount-modal input.form-control::-ms-input-placeholder {
    color:rgba(0, 0, 0, .3) !important;
}
body.nightmode input.form-control::placeholder {
    color:rgba(0, 0, 0, .3) !important;
}
body.nightmode input.form-control::-webkit-input-placeholder {
    color:rgba(0, 0, 0, .3) !important;
}
body.nightmode input.form-control:-moz-placeholder {
    color:rgba(0, 0, 0, .3)!important
}
body.nightmode input.form-control::-moz-placeholder {
    color:rgba(0, 0, 0, .3) !important;
}
body.nightmode input.form-control:-ms-input-placeholder {
    color:rgba(0, 0, 0, .3) !important;
}
body.nightmode input.form-control::-ms-input-placeholder {
    color:rgba(0, 0, 0, .3) !important;
}
body.nightmode .js-calendar, .js-calendar tbody {
    color:var(--HB);
}
body.nightmode .side-menu li.has_sub ul, body.nightmode .side-menu li.has_sub ul li a, body.nightmode .side-menu li.has_sub ul li.ms-hover, body.nightmode .side-menu li.has_sub ul li.ms-hover a {
    background-color:var(--70B) !important;
}
body.nightmode .side-menu li.has_sub ul li.ms-hover a:hover {
    background-color:var(--60B) !important;
	color:var(--00B) !important;
}
#sidebar-menu ul ul a {
    will-change:opacity, transform;
    -webkit-transition:all.3s ease-out;
    -moz-transition:all.3s ease-out;
    -o-transition:all.3s ease-out;
    -ms-transition:all.3s ease-out;
    transition:all.3s ease-out;
}
#sidebar-menu ul ul a:hover {
	background-color:var(--60B) !important;
    will-change:opacity, transform;
    -webkit-transition:all.3s ease-out;
    -moz-transition:all.3s ease-out;
    -o-transition:all.3s ease-out;
    -ms-transition:all.3s ease-out;
    transition:all.3s ease-out;
}
#sidebar-menu>ul>li>a.active, #sidebar-menu>ul>li>a:hover {
    border-left:2px solid var(--HB);
	background-color:var(--70B) !important;
}
#sidebar-menu ul li .menu-arrow {
    color:var(--10B);
}
.subdrop i, .subdrop span {
    color:var(--00B) !important;
}
body.nightmode .tabs-vertical-env ul.tabs-vertical:not(.active) {
    color:var(--10B) !important;
}
body.nightmode #setManualBuyButton.btn-success {
    background-color:var(--GRN) !important;
    border:1px solid var(--GRN) !important;
}
body.nightmode #setManualSellButton.btn-danger {
    background-color:var(--RED) !important;
    border:1px solid var(--RED) !important;
}
body.nightmode .content-page .page-title-box .btn-link {
    color: var(--70B) !important;
	margin-top: -11px !important;
}
body.nightmode .full_screen_tv_chart {
    background-color:var(--70B) !important;
    color:var(--10B) !important;
}
body.nightmode .collapse_div_left, body.nightmode .collapse_div_right {
    background-color:var(--80B) !important;
    color:var(--70B);
    border:1px dashed var(--70B);
}
body.nightmode .collapse_div_left:active, body.nightmode .collapse_div_right:active, body.nightmode .collapse_div_left:focus, body.nightmode .collapse_div_right:focus, body.nightmode .collapse_div_left:hover, body.nightmode .collapse_div_right:hover {
    background-color:var(--70B) !important;
    color:var(--60B);
    border:1px dashed var(--60B);
}
body.nightmode .nav-pills li.active a, .nav-pills li.active a:focus, .nav-pills li.active a:hover {
    color:var(--10B) !important;
}
body.nightmode .nav-pills>li>a {
    background-color:var(--60B);
    color:var(--10B) !important;
	will-change:opacity, transform;
    -webkit-transition:all.3s ease-out;
    -moz-transition:all.3s ease-out;
    -o-transition:all.3s ease-out;
    -ms-transition:all.3s ease-out;
    transition:all.3s ease-out;
}
body.nightmode .nav-pills li a:hover {
    color:var(--00B) !important;
    background-color:var(--HB) !important;
}
body.nightmode #select_correct_pos_to_buy.panel.panel-body, body.nightmode #select_correct_pos_to_sell.panel.panel-body {
    background:none !important;
}
body.nightmode .marketing_popup p.lead {
    color:var(--10B) !important;
}
body.nightmode .modal.modal-title {
    color:var(--10B) !important;
}
body.nightmode .list-group-item.active>.badge-success {
    color:var(--GRN);
	background-color:var(--00B) !important;
}
body.nightmode .list-group-item.active>.badge-danger {
    color:var(--RED);
	background-color:var(--00B) !important;
}
body.nightmode .col-md-9.col-sm-8 {
	border-left:1px solid var(--50B) !important;
	padding-left:15px;
}
body.nightmode .col-sm-7 {
    width:100%;
}
body.nightmode .col-sm-5 {
    width:50%;
}
body.nightmode .col-sm-4 {
    width:25%;
}
body.nightmode .col-sm-3 {
    width:25%;
}
.has-error .checkbox, .has-error .checkbox-inline, .has-error .control-label, .has-error .help-block, .has-error .radio, .has-error .radio-inline, .has-error.checkbox label, .has-error.checkbox-inline label, .has-error.radio label, .has-error.radio-inline label {
    color:var(--RED);
}
.table>thead>tr>th, body.nightmode .table>tbody>tr>td, body.nightmode .table>tbody>tr>th, body.nightmode .table>tfoot>tr>td, body.nightmode .table>tfoot>tr>th, body.nightmode .table>thead>tr>td {
    border-top:1px solid var(--50B);
}
body.nightmode .table-bordered>tbody>tr>td, .table-bordered>tbody>tr>th, .table-bordered>tfoot>tr>td, .table-bordered>tfoot>tr>th, .table-bordered>thead>tr>td, .table-bordered>thead>tr>th {
    border:1px solid var(--50B);
}
.table>thead>tr>th {
    border-bottom:1px solid var(--50B);
}
table.table-bordered.dataTable {
    border-collapse:collapse !important;
}

/* TradingView CSS */
/* Speedometer */

b, strong {
    font-family:SofiaPro-Bold,sans-serif;
}
.tv-error-card{
	display:flex;
	flex-direction:column;
	width:100%;
	height:100%;
	align-items:center;
	justify-content:center;
	color:#131722
}
html.theme-dark .tv-error-card{
	color:#d1d4dc
}
.tv-error-card__icon{
	display:flex;
	flex:0 0 auto;
	color:#b2b5be;
	margin-bottom:20px
}
.tv-error-card__message{
	font-size:24px;
	line-height:32px;
	font-weight:700
}
th{
	font-weight:400;
	letter-spacing:.2px
}
.table-2-juHm8n{
	margin-top:8px;
	width:100%
}
@media screen and (max-width:767px){
	.table-2-juHm8n{
		margin-top:0
}
}
.tableWrapper-2-juHm8n{
	width:100%
}
@media screen and (max-width:767px){
	.tableWrapper-2-juHm8n{
		overflow-x:auto;
		max-width:100%
}
}
.container-2-juHm8n{
	width:100%
}
.title-2-juHm8n,.title-2-juHm8n a{
	margin:40px 0 5px;
	color:#131722;
	font-size:20px;
	text-transform:uppercase;
	text-align:left;
	font-weight:700
}
html.theme-dark .title-2-juHm8n,html.theme-dark .title-2-juHm8n a{
	color:#b2b5be
}
@media screen and (max-width:767px){
	.title-2-juHm8n,.title-2-juHm8n a{
		margin:20px 0 5px
}
}
@media (any-hover:hover),(min--moz-device-pixel-ratio:0){
	.title-2-juHm8n a:hover{
		color:#2962ff
}
}
.header-2-juHm8n{
	height:40px;
	color:#787b86;
	font-size:12px
}
html.theme-dark .header-2-juHm8n{
	color:#787b86
}
.row-2-juHm8n{
	color:#131722;
	font-size:16px;
	border-bottom:1px solid;
	border-bottom-color:#f0f3fa
}
html.theme-dark .row-2-juHm8n{
	border-bottom-color:#2a2e39;
	color:#b2b5be
}
.row-2-juHm8n a{
	color:#131722;
	transition:color .35s ease
}
html.theme-dark .row-2-juHm8n a{
	color:#b2b5be
}
@media (any-hover:hover),(min--moz-device-pixel-ratio:0){
	.row-2-juHm8n a:hover,html.theme-dark .row-2-juHm8n a:hover{
		color:#2962ff
}
}
.cell-2-juHm8n{
	text-align:right;
	padding:10px 0 10px 28px
}
.cell-2-juHm8n:first-child{
	padding-left:0;
	text-align:left
}
.cell-2-juHm8n:not(:first-child){
	white-space:nowrap
}
@media screen and (max-width:767px){
	.cell-2-juHm8n{
		padding-left:12px
}
	.cell-2-juHm8n:not(:first-child){
		min-width:54px
}
}
@media screen and (max-width:479px){
	.cell-2-juHm8n:last-child{
		max-width:60px;
		overflow:hidden;
		text-overflow:ellipsis
}
}
.buyColor-2-juHm8n{
	color:#2962ff
}
.sellColor-2-juHm8n{
	color:#ef5350
}
.neutralColor-2-juHm8n{
	color:#787b86
}
@media screen and (max-width:1019px){
	.cell-2-juHm8n:first-child{
		padding:10px 0
}
}
.tv-data-mode{
	vertical-align:top
}
.tv-data-mode--realtime{
	color:#4db6ac
}
.tv-data-mode--snapshot{
	color:#3179f5
}
.tv-data-mode--endofday{
	color:#ab47bc
}
.tv-data-mode--connecting,.tv-data-mode--forbidden,.tv-data-mode--invalid,.tv-data-mode--loading{
	visibility:hidden
}
.tv-data-mode--delayed{
	color:#ff9800
}
.tv-data-mode--for-ticker-last{
	display:inline-block;
	font-size:12px;
	margin-left:2px;
	position:absolute;
	font-weight:700
}
.tv-data-mode--realtime--for-ticker-last{
	display:none
}
.tv-data-mode--for-ticker-tape{
	font-size:10px;
	transform:translateX(2px)
}
.tv-data-mode--realtime--for-ticker-tape{
	display:none
}
.tv-data-mode--for-ticker{
	display:inline-block;
	font-size:10px;
	margin-left:2px
}
.tv-data-mode--realtime--for-ticker,.tv-data-mode--realtime--no-realtime{
	display:none
}
.tv-data-mode--replay{
	color:#ff4a68
}
.tv-data-mode--for-chart{
	float:right;
	line-height:16px;
	margin-left:6px
}
.tv-data-mode--connecting--for-chart,.tv-data-mode--loading--for-chart{
	display:none
}
.tv-data-mode--forbidden--for-chart,.tv-data-mode--invalid--for-chart{
	color:#f44336;
	visibility:visible
}
.tv-data-mode--realtime--for-chart{
	display:none
}
.tv-data-mode--for-chart.tv-data-mode--replay{
	margin-left:0
}
.tv-data-mode--for-symbol-widget{
	display:inline;
	margin-left:3px;
	line-height:17px;
	font-size:15px
}
.tv-data-mode--realtime--for-symbol-widget,.tv-data-mode--realtime.tv-data-mode--for-symbol-widget{
	display:none
}
.tv-data-mode--for-watch-list{
	position:absolute;
	top:0;
	white-space:nowrap;
	overflow:visible;
	pointer-events:auto;
	margin:1.1em 2px 0;
	font-size:10px;
	left:100%
}
.tv-data-mode--realtime--for-watch-list{
	visibility:hidden
}
.tv-data-mode--size_large{
	font-size:12px
}
.tv-data-mode--for-symbol-info{
	display:inline;
	margin-left:3px;
	line-height:17px;
	font-size:15px
}
.tv-data-mode--realtime--for-symbol-info{
	display:none
}
.tv-data-mode--for-screener{
	font-size:10px
}
.tv-data-mode--realtime--for-screener{
	display:none
}
.common-tooltip-36YLR71G{
	display:inline-flex;
	position:fixed;
	color:#f0f3fa;
	font-size:12px;
	line-height:18px;
	opacity:1;
	transition:opacity .15s linear;
	z-index:1000;
	pointer-events:none
}
.common-tooltip--hidden-36YLR71G{
	opacity:0
}
.common-tooltip--horizontal-36YLR71G{
	margin:4px 0
}
.common-tooltip--horizontal-36YLR71G.common-tooltip--farther-36YLR71G{
	margin:8px 0
}
.common-tooltip--vertical-36YLR71G{
	margin:0 4px
}
.common-tooltip--vertical-36YLR71G.common-tooltip-farther-36YLR71G{
	margin:0 8px
}
.common-tooltip--no-pointer-events-36YLR71G{
	pointer-events:none
}
.common-tooltip--no-pointer-events-36YLR71G.common-tooltip--horizontal-36YLR71G{
	margin:8px 0
}
.common-tooltip--no-pointer-events-36YLR71G.common-tooltip--vertical-36YLR71G{
	margin:0 8px
}
.common-tooltip--no-pointer-events-36YLR71G.common-tooltip--horizontal-36YLR71G.common-tooltip--farther-36YLR71G{
	margin:14px 0
}
.common-tooltip--no-pointer-events-36YLR71G.common-tooltip--vertical-36YLR71G.common-tooltip--farther-36YLR71G{
	margin:0 14px
}
.common-tooltip--direction_normal-36YLR71G{
	flex-direction:row
}
.common-tooltip--direction_normal-36YLR71G .common-tooltip__body-36YLR71G{
	border-top-left-radius:2px;
	border-bottom-left-radius:2px
}
.common-tooltip--direction_normal-36YLR71G .common-tooltip__body--no-buttons-36YLR71G,.common-tooltip--direction_normal-36YLR71G .common-tooltip__button-container-36YLR71G{
	border-top-right-radius:2px;
	border-bottom-right-radius:2px
}
.common-tooltip--direction_normal-36YLR71G .common-tooltip__button-36YLR71G:not(:last-child){
	margin-right:1px
}
.common-tooltip--direction_reversed-36YLR71G{
	flex-direction:row-reverse
}
.common-tooltip--direction_reversed-36YLR71G .common-tooltip__body-36YLR71G{
	border-top-right-radius:2px;
	border-bottom-right-radius:2px
}
.common-tooltip--direction_reversed-36YLR71G .common-tooltip__body--no-buttons-36YLR71G,.common-tooltip--direction_reversed-36YLR71G .common-tooltip__button-container-36YLR71G{
	border-top-left-radius:2px;
	border-bottom-left-radius:2px
}
.common-tooltip--direction_reversed-36YLR71G .common-tooltip__button-36YLR71G:not(:first-child){
	margin-left:1px
}
.common-tooltip__ear-holder-36YLR71G{
	position:relative
}
.common-tooltip__ear-holder-36YLR71G:after{
	content:"";
	display:block;
	position:absolute;
	box-sizing:border-box;
	width:0;
	height:0;
	border:0 solid;
	border-color:#2a2e39
}
html.theme-dark .common-tooltip__ear-holder-36YLR71G:after{
	border-color:#50535e
}
.common-tooltip__ear-holder--above-36YLR71G:after,.common-tooltip__ear-holder--below-36YLR71G:after{
	left:50%;
	margin-left:-6px;
	border-left:6px solid;
	border-left-color:transparent;
	border-right:6px solid;
	border-right-color:transparent
}
html.theme-dark .common-tooltip__ear-holder--above-36YLR71G:after,html.theme-dark .common-tooltip__ear-holder--below-36YLR71G:after{
	border-right-color:transparent;
	border-left-color:transparent
}
.common-tooltip__ear-holder--below-36YLR71G:after{
	bottom:100%;
	border-bottom-width:4px
}
.common-tooltip__ear-holder--above-36YLR71G:after{
	top:100%;
	border-top-width:4px
}
.common-tooltip__ear-holder--after-36YLR71G:after,.common-tooltip__ear-holder--before-36YLR71G:after{
	top:50%;
	margin-top:-6px;
	border-top:6px solid;
	border-top-color:transparent;
	border-bottom:6px solid;
	border-bottom-color:transparent
}
html.theme-dark .common-tooltip__ear-holder--after-36YLR71G:after,html.theme-dark .common-tooltip__ear-holder--before-36YLR71G:after{
	border-bottom-color:transparent;
	border-top-color:transparent
}
.common-tooltip__ear-holder--before-36YLR71G:after{
	right:100%;
	border-right-width:4px
}
.common-tooltip__ear-holder--after-36YLR71G:after{
	left:100%;
	border-left-width:4px
}
.common-tooltip__body-36YLR71G{
	display:block;
	position:relative;
	box-sizing:border-box;
	padding:3px 8px;
	max-width:320px;
	background-color:#2a2e39;
	white-space:pre-wrap;
	word-wrap:break-word;
	text-align:left;
	overflow:hidden
}
html.theme-dark .common-tooltip__body-36YLR71G{
	background-color:#50535e
}
.common-tooltip__body--with-hotkey-36YLR71G{
	display:flex;
	max-width:420px;
	padding:0
}
.common-tooltip__body--width_wide-36YLR71G{
	max-width:640px
}
.common-tooltip__body--width_narrow-36YLR71G{
	max-width:200px
}
.common-tooltip__body--no-padding-36YLR71G{
	padding:0
}
.common-tooltip__hotkey-block-36YLR71G{
	display:inline-flex;
	flex:1 0 auto;
	padding:4px 8px 5px;
	line-height:12px;
	align-items:center;
	justify-content:center;
	color:#ff9800
}
.common-tooltip__hotkey-block--divider-36YLR71G{
	border-left:1px solid #5d606b;
	margin-left:8px
}
html.theme-dark .common-tooltip__hotkey-block--divider-36YLR71G{
	border-left:1px solid #363a45
}
.common-tooltip__hotkey-text-36YLR71G{
	display:inline-flex;
	align-items:center;
	margin:3px 0 3px 8px
}
.common-tooltip__hotkey-button-36YLR71G{
	display:inline-flex;
	justify-content:center;
	align-items:center;
	height:13px;
	min-width:7px;
	padding:0 3px;
	border:1px solid;
	border-radius:2px
}
.common-tooltip__plus-sign-36YLR71G{
	width:13px;
	height:15px;
	line-height:16px;
	text-align:center
}
.common-tooltip__button-container-36YLR71G{
	display:flex;
	position:relative;
	overflow:hidden
}
.common-tooltip__button-36YLR71G{
	display:flex;
	color:#fff;
	background-color:#2962ff;
	padding:0 10px;
	align-items:center
}
@media (any-hover:hover),(min--moz-device-pixel-ratio:0){
	.common-tooltip__button-36YLR71G:hover{
		background-color:#2962ff
}
}
.common-tooltip-36YLR71G.theme-white{
	color:#131722
}
html.theme-dark .common-tooltip-36YLR71G.theme-white{
	color:#d1d4dc
}
.common-tooltip-36YLR71G.theme-white .common-tooltip__body-36YLR71G{
	background-color:#fff;
	border-radius:0
}
html.theme-dark .common-tooltip-36YLR71G.theme-white .common-tooltip__body-36YLR71G{
	background-color:#1e222d
}
.common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder-36YLR71G{
	border:1px solid #dadde0
}
html.theme-dark .common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder-36YLR71G{
	border:1px solid #363c4e
}
.common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder-36YLR71G:after{
	border-color:#fff
}
html.theme-dark .common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder-36YLR71G:after{
	border-color:#1e222d
}
.common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--above-36YLR71G:after,.common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--below-36YLR71G:after{
	border-left:6px solid;
	border-left-color:transparent;
	border-right:6px solid;
	border-right-color:transparent
}
html.theme-dark .common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--above-36YLR71G:after,html.theme-dark .common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--below-36YLR71G:after{
	border-right-color:transparent;
	border-left-color:transparent
}
.common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--after-36YLR71G:after,.common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--before-36YLR71G:after{
	border-top:6px solid;
	border-top-color:transparent;
	border-bottom:6px solid;
	border-bottom-color:transparent
}
html.theme-dark .common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--after-36YLR71G:after,html.theme-dark .common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--before-36YLR71G:after{
	border-bottom-color:transparent;
	border-top-color:transparent
}
.common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder-36YLR71G:before{
	content:"";
	display:block;
	position:absolute;
	z-index:1000;
	width:0;
	height:0;
	border:0 solid;
	border-color:#dadde0
}
html.theme-dark .common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder-36YLR71G:before{
	border-color:#363c4e
}
.common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--above-36YLR71G:before,.common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--below-36YLR71G:before{
	left:50%;
	margin-left:-7px;
	border-left:7px solid;
	border-left-color:transparent;
	border-right:7px solid;
	border-right-color:transparent
}
html.theme-dark .common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--above-36YLR71G:before,html.theme-dark .common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--below-36YLR71G:before{
	border-right-color:transparent;
	border-left-color:transparent
}
.common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--below-36YLR71G:before{
	top:-6px;
	border-bottom-width:6px
}
.common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--above-36YLR71G:before{
	bottom:-6px;
	border-top-width:6px
}
.common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--after-36YLR71G:before,.common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--before-36YLR71G:before{
	top:50%;
	margin-top:-7px;
	border-top:7px solid;
	border-top-color:transparent;
	border-bottom:7px solid;
	border-bottom-color:transparent
}
html.theme-dark .common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--after-36YLR71G:before,html.theme-dark .common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--before-36YLR71G:before{
	border-bottom-color:transparent;
	border-top-color:transparent
}
.common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--before-36YLR71G:before{
	left:-6px;
	border-right-width:6px
}
.common-tooltip-36YLR71G.theme-white .common-tooltip__ear-holder--after-36YLR71G:before{
	right:-6px;
	border-left-width:6px
}
.common-tooltip-36YLR71G.theme-round-shadow{
	color:#131722;
	box-shadow:0 1px 3px 0 rgba(42,44,57,.29)
}
html.theme-dark .common-tooltip-36YLR71G.theme-round-shadow{
	color:#d1d4dc
}
.common-tooltip-36YLR71G.theme-round-shadow .common-tooltip__body-36YLR71G{
	background-color:#fff
}
html.theme-dark .common-tooltip-36YLR71G.theme-round-shadow .common-tooltip__body-36YLR71G{
	background-color:#1e222d
}
.common-tooltip-36YLR71G.theme-round-shadow .common-tooltip__ear-holder-36YLR71G:after{
	border-color:#fff
}
html.theme-dark .common-tooltip-36YLR71G.theme-round-shadow .common-tooltip__ear-holder-36YLR71G:after{
	border-color:#1e222d
}
.common-tooltip-36YLR71G.theme-round-shadow .common-tooltip__ear-holder--above-36YLR71G:after,.common-tooltip-36YLR71G.theme-round-shadow .common-tooltip__ear-holder--below-36YLR71G:after{
	border-left:6px solid;
	border-left-color:transparent;
	border-right:6px solid;
	border-right-color:transparent
}
html.theme-dark .common-tooltip-36YLR71G.theme-round-shadow .common-tooltip__ear-holder--above-36YLR71G:after,html.theme-dark .common-tooltip-36YLR71G.theme-round-shadow .common-tooltip__ear-holder--below-36YLR71G:after{
	border-right-color:transparent;
	border-left-color:transparent
}
.common-tooltip-36YLR71G.theme-round-shadow .common-tooltip__ear-holder--after-36YLR71G:after,.common-tooltip-36YLR71G.theme-round-shadow .common-tooltip__ear-holder--before-36YLR71G:after{
	border-top:6px solid;
	border-top-color:transparent;
	border-bottom:6px solid;
	border-bottom-color:transparent
}
html.theme-dark .common-tooltip-36YLR71G.theme-round-shadow .common-tooltip__ear-holder--after-36YLR71G:after,html.theme-dark .common-tooltip-36YLR71G.theme-round-shadow .common-tooltip__ear-holder--before-36YLR71G:after{
	border-bottom-color:transparent;
	border-top-color:transparent
}
.container-2qn7A4BC{
	display:flex;
	justify-content:center;
	width:100%
}
.speedometerWrapper-2qn7A4BC{
	display:flex;
	position:relative;
	flex-direction:column;
	align-items:center
}
.speedometerTextWrapper-2qn7A4BC{
	display:flex;
	position:absolute;
	flex-direction:column;
	width:100%;
	left:0;
	align-items:center
}
.speedometerText-2qn7A4BC{
	display:flex;
	position:relative;
	width:52px;
	justify-content:center;
	font-size:10px;
	text-transform:uppercase;
	font-weight:700;
	letter-spacing:.4px;
	color:#131722
}
html.theme-dark .speedometerText-2qn7A4BC{
	color:var(--10B);
}
.speedometerTextMono-2qn7A4BC{
	font-weight:400;
	color:#787b86
}
.textTop-2qn7A4BC{
	width:100%;
	text-align:center
}
.textBottom-2qn7A4BC{
	display:flex;
	flex-direction:column;
	align-items:stretch;
	margin:0
}
.textBottomWrap-2qn7A4BC{
	display:flex;
	justify-content:center;
	width:100%
}
.bottomSignals-2qn7A4BC,.middleSignals-2qn7A4BC{
	display:flex;
	justify-content:space-between;
	margin:20px 0
}
.middleSignals-2qn7A4BC{
	width:114%
}
.bottomSignals-2qn7A4BC{
	width:153%;
	text-align:center
}
.sizeWrapper-2qn7A4BC{
	position:relative;
	width:220px;
	height:110px;
	overflow:hidden;
	margin-top:20px
}
.circleWrapper-2qn7A4BC{
	position:relative;
	width:220px;
	height:110px;
	background-image:url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbDpzcGFjZT0icHJlc2VydmUiIHdpZHRoPSIyMjBweCIgaGVpZ2h0PSIxMTBweCIgdmVyc2lvbj0iMS4xIiBzdHlsZT0ic2hhcGUtcmVuZGVyaW5nOmdlb21ldHJpY1ByZWNpc2lvbjsgdGV4dC1yZW5kZXJpbmc6Z2VvbWV0cmljUHJlY2lzaW9uOyBpbWFnZS1yZW5kZXJpbmc6b3B0aW1pemVRdWFsaXR5OyBmaWxsLXJ1bGU6ZXZlbm9kZDsgY2xpcC1ydWxlOmV2ZW5vZGQiCnZpZXdCb3g9IjAgMCAzOS43MyAxOS44NiIKIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIj4KIDxkZWZzPgogIDxzdHlsZSB0eXBlPSJ0ZXh0L2NzcyI+CiAgIDwhW0NEQVRBWwogICAgLmZpbDY0IHtmaWxsOiMwMEIyQzZ9CiAgICAuZmlsNjMge2ZpbGw6IzAwQjJDOH0KICAgIC5maWw2NyB7ZmlsbDojMDBCM0MwfQogICAgLmZpbDY2IHtmaWxsOiMwMEIzQzJ9CiAgICAuZmlsNjUge2ZpbGw6IzAwQjNDNH0KICAgIC5maWw3MCB7ZmlsbDojMDBCNEJCfQogICAgLmZpbDY5IHtmaWxsOiMwMEI0QkR9CiAgICAuZmlsNjgge2ZpbGw6IzAwQjRCRn0KICAgIC5maWw3MyB7ZmlsbDojMDBCNUI2fQogICAgLmZpbDcyIHtmaWxsOiMwMEI1Qjh9CiAgICAuZmlsNzEge2ZpbGw6IzAwQjVCOX0KICAgIC5maWw3NiB7ZmlsbDojMDBCNkIxfQogICAgLmZpbDc1IHtmaWxsOiMwMEI2QjJ9CiAgICAuZmlsNzQge2ZpbGw6IzAwQjZCNH0KICAgIC5maWw3OSB7ZmlsbDojMDBCN0FCfQogICAgLmZpbDc4IHtmaWxsOiMwMEI3QUR9CiAgICAuZmlsNzcge2ZpbGw6IzAwQjdBRn0KICAgIC5maWw4MiB7ZmlsbDojMDBCOEE2fQogICAgLmZpbDgxIHtmaWxsOiMwMEI4QTh9CiAgICAuZmlsODAge2ZpbGw6IzAwQjhBOX0KICAgIC5maWw4NSB7ZmlsbDojMDBCOUExfQogICAgLmZpbDg0IHtmaWxsOiMwMEI5QTJ9CiAgICAuZmlsODMge2ZpbGw6IzAwQjlBNH0KICAgIC5maWw4OCB7ZmlsbDojMDBCQTlCfQogICAgLmZpbDg3IHtmaWxsOiMwMEJBOUR9CiAgICAuZmlsODYge2ZpbGw6IzAwQkE5Rn0KICAgIC5maWw5MSB7ZmlsbDojMDBCQjk2fQogICAgLmZpbDkwIHtmaWxsOiMwMEJCOTh9CiAgICAuZmlsODkge2ZpbGw6IzAwQkI5OX0KICAgIC5maWw5NCB7ZmlsbDojMDBCQzkxfQogICAgLmZpbDkzIHtmaWxsOiMwMEJDOTJ9CiAgICAuZmlsOTIge2ZpbGw6IzAwQkM5NH0KICAgIC5maWw5NyB7ZmlsbDojMDBCRDhCfQogICAgLmZpbDk2IHtmaWxsOiMwMEJEOER9CiAgICAuZmlsOTUge2ZpbGw6IzAwQkQ4Rn0KICAgIC5maWwxMDAge2ZpbGw6IzAwQkU4Nn0KICAgIC5maWw5OSB7ZmlsbDojMDBCRTg4fQogICAgLmZpbDk4IHtmaWxsOiMwMEJFOEF9CiAgICAuZmlsMTAzIHtmaWxsOiMwMEJGODF9CiAgICAuZmlsMTAyIHtmaWxsOiMwMEJGODJ9CiAgICAuZmlsMTAxIHtmaWxsOiMwMEJGODR9CiAgICAuZmlsMTA2IHtmaWxsOiMwMEMwN0J9CiAgICAuZmlsMTA1IHtmaWxsOiMwMEMwN0R9CiAgICAuZmlsMTA0IHtmaWxsOiMwMEMwN0Z9CiAgICAuZmlsMTA5IHtmaWxsOiMwMEMxNzZ9CiAgICAuZmlsMTA4IHtmaWxsOiMwMEMxNzh9CiAgICAuZmlsMTA3IHtmaWxsOiMwMEMxN0F9CiAgICAuZmlsMTEyIHtmaWxsOiMwMEMyNzF9CiAgICAuZmlsMTExIHtmaWxsOiMwMEMyNzJ9CiAgICAuZmlsMTEwIHtmaWxsOiMwMEMyNzR9CiAgICAuZmlsMTE1IHtmaWxsOiMwMEMzNkJ9CiAgICAuZmlsMTE0IHtmaWxsOiMwMEMzNkR9CiAgICAuZmlsMTEzIHtmaWxsOiMwMEMzNkZ9CiAgICAuZmlsMTE4IHtmaWxsOiMwMEM0NjZ9CiAgICAuZmlsMTE3IHtmaWxsOiMwMEM0Njh9CiAgICAuZmlsMTE2IHtmaWxsOiMwMEM0NkF9CiAgICAuZmlsMTIxIHtmaWxsOiMwMEM1NjF9CiAgICAuZmlsMTIwIHtmaWxsOiMwMEM1NjN9CiAgICAuZmlsMTE5IHtmaWxsOiMwMEM1NjR9CiAgICAuZmlsMTI0IHtmaWxsOiMwMEM2NUJ9CiAgICAuZmlsMTIzIHtmaWxsOiMwMEM2NUR9CiAgICAuZmlsMTIyIHtmaWxsOiMwMEM2NUZ9CiAgICAuZmlsMTI3IHtmaWxsOiMwMEM3NTd9CiAgICAuZmlsMTI2IHtmaWxsOiMwMEM3NTh9CiAgICAuZmlsMTI1IHtmaWxsOiMwMEM3NUF9CiAgICAuZmlsNjIge2ZpbGw6IzAzQjBDNn0KICAgIC5maWw2MSB7ZmlsbDojMDdBREM0fQogICAgLmZpbDYwIHtmaWxsOiMwQkFBQzJ9CiAgICAuZmlsNTkge2ZpbGw6IzBGQThDMH0KICAgIC5maWw1OCB7ZmlsbDojMTNBNUJFfQogICAgLmZpbDU3IHtmaWxsOiMxN0EyQkN9CiAgICAuZmlsNTYge2ZpbGw6IzFCOUZCQX0KICAgIC5maWw1NSB7ZmlsbDojMUY5Q0I3fQogICAgLmZpbDU0IHtmaWxsOiMyMzlBQjV9CiAgICAuZmlsNTMge2ZpbGw6IzI3OTdCM30KICAgIC5maWw1MiB7ZmlsbDojMkI5NEIxfQogICAgLmZpbDUxIHtmaWxsOiMyRjkxQUZ9CiAgICAuZmlsNTAge2ZpbGw6IzMzOEVBRH0KICAgIC5maWw0OSB7ZmlsbDojMzc4Q0FCfQogICAgLmZpbDQ4IHtmaWxsOiMzQjg5QTl9CiAgICAuZmlsNDcge2ZpbGw6IzNGODZBNn0KICAgIC5maWw0NiB7ZmlsbDojNDM4M0E0fQogICAgLmZpbDQ1IHtmaWxsOiM0NzgwQTJ9CiAgICAuZmlsNDQge2ZpbGw6IzRCN0VBMH0KICAgIC5maWw0MyB7ZmlsbDojNEY3QjlFfQogICAgLmZpbDQyIHtmaWxsOiM1Mzc4OUN9CiAgICAuZmlsNDEge2ZpbGw6IzU3NzU5QX0KICAgIC5maWw0MCB7ZmlsbDojNUI3Mjk3fQogICAgLmZpbDM5IHtmaWxsOiM1RjcwOTV9CiAgICAuZmlsMzgge2ZpbGw6IzYzNkQ5M30KICAgIC5maWwzNyB7ZmlsbDojNjc2QTkxfQogICAgLmZpbDM2IHtmaWxsOiM2QjY3OEZ9CiAgICAuZmlsMzUge2ZpbGw6IzZGNjU4RH0KICAgIC5maWwzNCB7ZmlsbDojNzM2MjhCfQogICAgLmZpbDMzIHtmaWxsOiM3NzVGODl9CiAgICAuZmlsMzIge2ZpbGw6IzdCNUM4Nn0KICAgIC5maWwzMSB7ZmlsbDojN0Y1OTg0fQogICAgLmZpbDMwIHtmaWxsOiM4MzU3ODJ9CiAgICAuZmlsMjkge2ZpbGw6Izg3NTQ4MH0KICAgIC5maWwyOCB7ZmlsbDojOEI1MTdFfQogICAgLmZpbDI3IHtmaWxsOiM4RjRFN0N9CiAgICAuZmlsMjYge2ZpbGw6IzkzNEI3QX0KICAgIC5maWwyNSB7ZmlsbDojOTc0OTc3fQogICAgLmZpbDI0IHtmaWxsOiM5QjQ2NzV9CiAgICAuZmlsMjMge2ZpbGw6IzlGNDM3M30KICAgIC5maWwyMiB7ZmlsbDojQTM0MDcxfQogICAgLmZpbDIxIHtmaWxsOiNBNzNENkZ9CiAgICAuZmlsMjAge2ZpbGw6I0FCM0I2RH0KICAgIC5maWwxOSB7ZmlsbDojQUYzODZCfQogICAgLmZpbDE4IHtmaWxsOiNCMzM1Njl9CiAgICAuZmlsMTcge2ZpbGw6I0I3MzI2Nn0KICAgIC5maWwxNiB7ZmlsbDojQkIyRjY0fQogICAgLmZpbDE1IHtmaWxsOiNCRjJENjJ9CiAgICAuZmlsMTQge2ZpbGw6I0MzMkE2MH0KICAgIC5maWwxMyB7ZmlsbDojQzcyNzVFfQogICAgLmZpbDEyIHtmaWxsOiNDQjI0NUN9CiAgICAuZmlsMTEge2ZpbGw6I0NGMjI1QX0KICAgIC5maWwxMCB7ZmlsbDojRDMxRjU3fQogICAgLmZpbDkge2ZpbGw6I0Q3MUM1NX0KICAgIC5maWw4IHtmaWxsOiNEQjE5NTN9CiAgICAuZmlsNyB7ZmlsbDojREYxNjUxfQogICAgLmZpbDYge2ZpbGw6I0UzMTQ0Rn0KICAgIC5maWw1IHtmaWxsOiNFNzExNER9CiAgICAuZmlsNCB7ZmlsbDojRUIwRTRCfQogICAgLmZpbDMge2ZpbGw6I0VGMEI0OX0KICAgIC5maWwyIHtmaWxsOiNGMzA4NDZ9CiAgICAuZmlsMSB7ZmlsbDojRjcwNjQ0fQogICAgLmZpbDAge2ZpbGw6I0ZCMDM0Mn0KICAgIC5maWwxMjgge2ZpbGw6I0ZGMDA0MH0KICAgXV0+CiAgPC9zdHlsZT4KICAgIDxjbGlwUGF0aCBpZD0iaWQwIj4KICAgICA8cGF0aCBkPSJNMy41IDguNmMwLjA1LC0wLjA3IDAuMTIsLTAuMTEgMC4yLC0wLjExIDAuMDYsMCAwLjExLDAuMDIgMC4xNSwwLjA1IDAuMTEsMC4wOCAwLjE0LDAuMjQgMC4wNiwwLjM1IC0yLjE3LDMuMTUgLTMuMzYsNi44OSAtMy40MSwxMC43MiAwLDAuMTQgLTAuMTEsMC4yNSAtMC4yNSwwLjI1IC0wLjE0LDAgLTAuMjUsLTAuMTEgLTAuMjUsLTAuMjUgMCwwIDAsMCAwLDAgMC4wNSwtNC4wOCAxLjM0LC03Ljg3IDMuNSwtMTEuMDFsMCAwem0zMi4zOCAtMC4wNmMtMC4wNywwLjA1IC0wLjExLDAuMTMgLTAuMTEsMC4yMSAwLDAuMDUgMC4wMiwwLjEgMC4wNSwwLjE0IDIuMTcsMy4xNSAzLjM2LDYuODkgMy40LDEwLjcyIDAsMC4xNCAwLjEyLDAuMjUgMC4yNiwwLjI1IDAuMTQsMCAwLjI1LC0wLjExIDAuMjUsLTAuMjUgMCwwIDAsMCAwLDAgLTAuMDQsLTMuOTMgLTEuMjcsLTcuNzcgLTMuNSwtMTEuMDEgLTAuMDUsLTAuMDcgLTAuMTIsLTAuMTEgLTAuMjEsLTAuMTEgLTAuMDUsMCAtMC4xLDAuMDIgLTAuMTQsMC4wNWwwIDB6bS05LjQ5IC02LjkxYy0wLjExLC0wLjA0IC0wLjE3LC0wLjEzIC0wLjE3LC0wLjI0IDAsLTAuMDMgMCwtMC4wNSAwLjAxLC0wLjA4IDAuMDMsLTAuMSAwLjEzLC0wLjE3IDAuMjQsLTAuMTcgMC4wMiwwIDAuMDUsMCAwLjA4LDAuMDEgMy42LDEuMjkgNi43NiwzLjYgOS4wOCw2LjYzIDAuMDksMC4xMSAwLjA2LDAuMjcgLTAuMDUsMC4zNSAtMC4wNCwwLjA0IC0wLjEsMC4wNSAtMC4xNSwwLjA1IC0wLjA4LDAgLTAuMTUsLTAuMDMgLTAuMiwtMC4xIC0yLjI3LC0yLjk1IC01LjM0LC01LjE5IC04Ljg0LC02LjQ1bDAgMHptLTEyLjQyIC0wLjQ4YzAuMDQsMC4xMSAwLjE0LDAuMTggMC4yNSwwLjE4IDAuMDIsMCAwLjA1LC0wLjAxIDAuMDcsLTAuMDEgMS44LC0wLjU0IDMuNjcsLTAuODIgNS41NiwtMC44MiAwLDAgMC4wMSwwIDAuMDEsMCAxLjk0LDAgMy44MSwwLjI5IDUuNTgsMC44MiAwLjAyLDAgMC4wNSwwLjAxIDAuMDcsMC4wMSAwLjExLDAgMC4yMSwtMC4wNyAwLjI0LC0wLjE4IDAuMDEsLTAuMDIgMC4wMSwtMC4wNSAwLjAxLC0wLjA3IDAsLTAuMTEgLTAuMDcsLTAuMjEgLTAuMTcsLTAuMjQgLTEuODUsLTAuNTYgLTMuNzgsLTAuODQgLTUuNzEsLTAuODQgMCwwIC0wLjAxLDAgLTAuMDIsMCAtMS45OSwwIC0zLjkxLDAuMjkgLTUuNzIsMC44NCAtMC4xMSwwLjAzIC0wLjE4LDAuMTMgLTAuMTgsMC4yNCAwLDAuMDIgMC4wMSwwLjA1IDAuMDIsMC4wN2wtMC4wMSAwem0tMC40NyAwLjE2YzAuMDEsMC4wMyAwLjAxLDAuMDUgMC4wMSwwLjA4IDAsMC4xMSAtMC4wNywwLjIgLTAuMTcsMC4yNCAtMy41LDEuMjUgLTYuNTgsMy41IC04Ljg0LDYuNDUgLTAuMDUsMC4wNyAtMC4xMiwwLjEgLTAuMiwwLjEgLTAuMDYsMCAtMC4xMSwtMC4wMSAtMC4xNSwtMC4wNSAtMC4wNywtMC4wNCAtMC4xLC0wLjEyIC0wLjEsLTAuMiAwLC0wLjA1IDAuMDEsLTAuMSAwLjA1LC0wLjE1IDIuMzIsLTMuMDMgNS40OCwtNS4zNCA5LjA4LC02LjYzIDAuMTMsLTAuMDQgMC4yNywwLjAzIDAuMzIsMC4xNmwwIDB6Ii8+CiAgICA8L2NsaXBQYXRoPgogPC9kZWZzPgogPGcgaWQ9IjEiPgogIDxnPgogICA8ZyBzdHlsZT0iY2xpcC1wYXRoOnVybCgjaWQwKSI+CiAgICA8cG9seWdvbiBjbGFzcz0iZmlsMCIgcG9pbnRzPSIyMC4xOCwxOS44MyAtOC4xMiwxOS43MSAtOC4xMSwxOC42NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxIiBjbGFzcz0iZmlsMSIgcG9pbnRzPSIyMC4xOCwxOS44MyAtOC4xMiwxOC44NCAtOC4wOSwxNy45NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyIiBjbGFzcz0iZmlsMiIgcG9pbnRzPSIyMC4xOCwxOS44MyAtOC4xLDE4LjE1IC04LjA1LDE3LjI4ICIvPgogICAgPHBvbHlnb24gaWQ9IjMiIGNsYXNzPSJmaWwzIiBwb2ludHM9IjIwLjE4LDE5LjgzIC04LjA2LDE3LjQ1IC03Ljk5LDE2LjU5ICIvPgogICAgPHBvbHlnb24gaWQ9IjQiIGNsYXNzPSJmaWw0IiBwb2ludHM9IjIwLjE4LDE5LjgzIC04LjAxLDE2Ljc2IC03LjkyLDE1LjkgIi8+CiAgICA8cG9seWdvbiBpZD0iNSIgY2xhc3M9ImZpbDUiIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuOTMsMTYuMDcgLTcuODMsMTUuMjEgIi8+CiAgICA8cG9seWdvbiBpZD0iNiIgY2xhc3M9ImZpbDYiIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuODUsMTUuMzkgLTcuNzIsMTQuNTMgIi8+CiAgICA8cG9seWdvbiBpZD0iNyIgY2xhc3M9ImZpbDciIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuNzQsMTQuNyAtNy41OSwxMy44NSAiLz4KICAgIDxwb2x5Z29uIGlkPSI4IiBjbGFzcz0iZmlsOCIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNy42MiwxNC4wMiAtNy40NSwxMy4xNyAiLz4KICAgIDxwb2x5Z29uIGlkPSI5IiBjbGFzcz0iZmlsOSIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNy40OCwxMy4zNCAtNy4yOSwxMi41ICIvPgogICAgPHBvbHlnb24gaWQ9IjEwIiBjbGFzcz0iZmlsMTAiIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuMzMsMTIuNjcgLTcuMTEsMTEuODMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTEiIGNsYXNzPSJmaWwxMSIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNy4xNiwxMiAtNi45MiwxMS4xNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMiIgY2xhc3M9ImZpbDEyIiBwb2ludHM9IjIwLjE4LDE5LjgzIC02Ljk3LDExLjMzIC02LjcxLDEwLjUxICIvPgogICAgPHBvbHlnb24gaWQ9IjEzIiBjbGFzcz0iZmlsMTMiIHBvaW50cz0iMjAuMTgsMTkuODMgLTYuNzcsMTAuNjcgLTYuNDksOS44NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNCIgY2xhc3M9ImZpbDE0IiBwb2ludHM9IjIwLjE4LDE5LjgzIC02LjU0LDEwLjAyIC02LjI1LDkuMjEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTUiIGNsYXNzPSJmaWwxNSIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNi4zMSw5LjM3IC01Ljk5LDguNTcgIi8+CiAgICA8cG9seWdvbiBpZD0iMTYiIGNsYXNzPSJmaWwxNiIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNi4wNiw4LjczIC01LjcyLDcuOTQgIi8+CiAgICA8cG9seWdvbiBpZD0iMTciIGNsYXNzPSJmaWwxNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNS43OSw4LjA5IC01LjQzLDcuMzEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTgiIGNsYXNzPSJmaWwxOCIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNS41LDcuNDcgLTUuMTMsNi42OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOSIgY2xhc3M9ImZpbDE5IiBwb2ludHM9IjIwLjE4LDE5LjgzIC01LjIsNi44NSAtNC44MSw2LjA4ICIvPgogICAgPHBvbHlnb24gaWQ9IjIwIiBjbGFzcz0iZmlsMjAiIHBvaW50cz0iMjAuMTgsMTkuODMgLTQuODksNi4yMyAtNC40OCw1LjQ4ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxIiBjbGFzcz0iZmlsMjEiIHBvaW50cz0iMjAuMTgsMTkuODMgLTQuNTYsNS42MyAtNC4xMyw0Ljg4ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyIiBjbGFzcz0iZmlsMjIiIHBvaW50cz0iMjAuMTgsMTkuODMgLTQuMjIsNS4wMyAtMy43Nyw0LjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjMiIGNsYXNzPSJmaWwyMyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMy44Niw0LjQ0IC0zLjM5LDMuNzIgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQiIGNsYXNzPSJmaWwyNCIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMy40OCwzLjg3IC0zLDMuMTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMjUiIGNsYXNzPSJmaWwyNSIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMy4wOSwzLjMgLTIuNTksMi42ICIvPgogICAgPHBvbHlnb24gaWQ9IjI2IiBjbGFzcz0iZmlsMjYiIHBvaW50cz0iMjAuMTgsMTkuODMgLTIuNjksMi43NCAtMi4xNywyLjA1ICIvPgogICAgPHBvbHlnb24gaWQ9IjI3IiBjbGFzcz0iZmlsMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTIuMjgsMi4xOSAtMS43NCwxLjUyICIvPgogICAgPHBvbHlnb24gaWQ9IjI4IiBjbGFzcz0iZmlsMjgiIHBvaW50cz0iMjAuMTgsMTkuODMgLTEuODUsMS42NSAtMS4yOSwwLjk5ICIvPgogICAgPHBvbHlnb24gaWQ9IjI5IiBjbGFzcz0iZmlsMjkiIHBvaW50cz0iMjAuMTgsMTkuODMgLTEuNCwxLjEzIC0wLjgzLDAuNDggIi8+CiAgICA8cG9seWdvbiBpZD0iMzAiIGNsYXNzPSJmaWwzMCIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMC45NSwwLjYxIC0wLjM2LC0wLjAyICIvPgogICAgPHBvbHlnb24gaWQ9IjMxIiBjbGFzcz0iZmlsMzEiIHBvaW50cz0iMjAuMTgsMTkuODMgLTAuNDgsMC4xMSAwLjEyLC0wLjUxICIvPgogICAgPHBvbHlnb24gaWQ9IjMyIiBjbGFzcz0iZmlsMzIiIHBvaW50cz0iMjAuMTgsMTkuODMgMCwtMC4zOSAwLjYyLC0wLjk4ICIvPgogICAgPHBvbHlnb24gaWQ9IjMzIiBjbGFzcz0iZmlsMzMiIHBvaW50cz0iMjAuMTgsMTkuODMgMC40OSwtMC44NiAxLjEyLC0xLjQ1ICIvPgogICAgPHBvbHlnb24gaWQ9IjM0IiBjbGFzcz0iZmlsMzQiIHBvaW50cz0iMjAuMTgsMTkuODMgMSwtMS4zMyAxLjY0LC0xLjkgIi8+CiAgICA8cG9seWdvbiBpZD0iMzUiIGNsYXNzPSJmaWwzNSIgcG9pbnRzPSIyMC4xOCwxOS44MyAxLjUxLC0xLjc5IDIuMTcsLTIuMzQgIi8+CiAgICA8cG9seWdvbiBpZD0iMzYiIGNsYXNzPSJmaWwzNiIgcG9pbnRzPSIyMC4xOCwxOS44MyAyLjA0LC0yLjIzIDIuNzIsLTIuNzYgIi8+CiAgICA8cG9seWdvbiBpZD0iMzciIGNsYXNzPSJmaWwzNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyLjU4LC0yLjY2IDMuMjcsLTMuMTcgIi8+CiAgICA8cG9seWdvbiBpZD0iMzgiIGNsYXNzPSJmaWwzOCIgcG9pbnRzPSIyMC4xOCwxOS44MyAzLjEzLC0zLjA3IDMuODMsLTMuNTcgIi8+CiAgICA8cG9seWdvbiBpZD0iMzkiIGNsYXNzPSJmaWwzOSIgcG9pbnRzPSIyMC4xOCwxOS44MyAzLjY5LC0zLjQ3IDQuNCwtMy45NiAiLz4KICAgIDxwb2x5Z29uIGlkPSI0MCIgY2xhc3M9ImZpbDQwIiBwb2ludHM9IjIwLjE4LDE5LjgzIDQuMjYsLTMuODYgNC45OCwtNC4zMiAiLz4KICAgIDxwb2x5Z29uIGlkPSI0MSIgY2xhc3M9ImZpbDQxIiBwb2ludHM9IjIwLjE4LDE5LjgzIDQuODQsLTQuMjMgNS41NywtNC42OCAiLz4KICAgIDxwb2x5Z29uIGlkPSI0MiIgY2xhc3M9ImZpbDQyIiBwb2ludHM9IjIwLjE4LDE5LjgzIDUuNDMsLTQuNTkgNi4xNywtNS4wMiAiLz4KICAgIDxwb2x5Z29uIGlkPSI0MyIgY2xhc3M9ImZpbDQzIiBwb2ludHM9IjIwLjE4LDE5LjgzIDYuMDIsLTQuOTMgNi43OCwtNS4zNCAiLz4KICAgIDxwb2x5Z29uIGlkPSI0NCIgY2xhc3M9ImZpbDQ0IiBwb2ludHM9IjIwLjE4LDE5LjgzIDYuNjMsLTUuMjYgNy40LC01LjY1ICIvPgogICAgPHBvbHlnb24gaWQ9IjQ1IiBjbGFzcz0iZmlsNDUiIHBvaW50cz0iMjAuMTgsMTkuODMgNy4yNCwtNS41OCA4LjAyLC01Ljk1ICIvPgogICAgPHBvbHlnb24gaWQ9IjQ2IiBjbGFzcz0iZmlsNDYiIHBvaW50cz0iMjAuMTgsMTkuODMgNy44NiwtNS44NyA4LjY1LC02LjIzICIvPgogICAgPHBvbHlnb24gaWQ9IjQ3IiBjbGFzcz0iZmlsNDciIHBvaW50cz0iMjAuMTgsMTkuODMgOC40OSwtNi4xNiA5LjI5LC02LjQ5ICIvPgogICAgPHBvbHlnb24gaWQ9IjQ4IiBjbGFzcz0iZmlsNDgiIHBvaW50cz0iMjAuMTgsMTkuODMgOS4xMywtNi40MiA5LjkzLC02Ljc0ICIvPgogICAgPHBvbHlnb24gaWQ9IjQ5IiBjbGFzcz0iZmlsNDkiIHBvaW50cz0iMjAuMTgsMTkuODMgOS43NywtNi42NyAxMC41OCwtNi45NyAiLz4KICAgIDxwb2x5Z29uIGlkPSI1MCIgY2xhc3M9ImZpbDUwIiBwb2ludHM9IjIwLjE4LDE5LjgzIDEwLjQyLC02LjkxIDExLjI0LC03LjE4ICIvPgogICAgPHBvbHlnb24gaWQ9IjUxIiBjbGFzcz0iZmlsNTEiIHBvaW50cz0iMjAuMTgsMTkuODMgMTEuMDgsLTcuMTMgMTEuOSwtNy4zOCAiLz4KICAgIDxwb2x5Z29uIGlkPSI1MiIgY2xhc3M9ImZpbDUyIiBwb2ludHM9IjIwLjE4LDE5LjgzIDExLjc0LC03LjMzIDEyLjU3LC03LjU2ICIvPgogICAgPHBvbHlnb24gaWQ9IjUzIiBjbGFzcz0iZmlsNTMiIHBvaW50cz0iMjAuMTgsMTkuODMgMTIuNCwtNy41MiAxMy4yNCwtNy43MyAiLz4KICAgIDxwb2x5Z29uIGlkPSI1NCIgY2xhc3M9ImZpbDU0IiBwb2ludHM9IjIwLjE4LDE5LjgzIDEzLjA3LC03LjY5IDEzLjkxLC03Ljg4ICIvPgogICAgPHBvbHlnb24gaWQ9IjU1IiBjbGFzcz0iZmlsNTUiIHBvaW50cz0iMjAuMTgsMTkuODMgMTMuNzUsLTcuODQgMTQuNTksLTguMDEgIi8+CiAgICA8cG9seWdvbiBpZD0iNTYiIGNsYXNzPSJmaWw1NiIgcG9pbnRzPSIyMC4xOCwxOS44MyAxNC40MiwtNy45OCAxNS4yOCwtOC4xMyAiLz4KICAgIDxwb2x5Z29uIGlkPSI1NyIgY2xhc3M9ImZpbDU3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDE1LjExLC04LjEgMTUuOTYsLTguMjMgIi8+CiAgICA8cG9seWdvbiBpZD0iNTgiIGNsYXNzPSJmaWw1OCIgcG9pbnRzPSIyMC4xOCwxOS44MyAxNS43OSwtOC4yIDE2LjY1LC04LjMxICIvPgogICAgPHBvbHlnb24gaWQ9IjU5IiBjbGFzcz0iZmlsNTkiIHBvaW50cz0iMjAuMTgsMTkuODMgMTYuNDgsLTguMjkgMTcuMzQsLTguMzcgIi8+CiAgICA8cG9seWdvbiBpZD0iNjAiIGNsYXNzPSJmaWw2MCIgcG9pbnRzPSIyMC4xOCwxOS44MyAxNy4xNywtOC4zNiAxOC4wMywtOC40MiAiLz4KICAgIDxwb2x5Z29uIGlkPSI2MSIgY2xhc3M9ImZpbDYxIiBwb2ludHM9IjIwLjE4LDE5LjgzIDE3Ljg2LC04LjQxIDE4LjczLC04LjQ1ICIvPgogICAgPHBvbHlnb24gaWQ9IjYyIiBjbGFzcz0iZmlsNjIiIHBvaW50cz0iMjAuMTgsMTkuODMgMTguNTUsLTguNDUgMTkuNDIsLTguNDcgIi8+CiAgICA8cG9seWdvbiBpZD0iNjMiIGNsYXNzPSJmaWw2MyIgcG9pbnRzPSIyMC4xOCwxOS44MyAxOS4yNSwtOC40NiAyMC4xMSwtOC40NyAiLz4KICAgIDxwb2x5Z29uIGlkPSI2NCIgY2xhc3M9ImZpbDY0IiBwb2ludHM9IjIwLjE4LDE5LjgzIDE5Ljk0LC04LjQ2IDIwLjgxLC04LjQ1ICIvPgogICAgPHBvbHlnb24gaWQ9IjY1IiBjbGFzcz0iZmlsNjUiIHBvaW50cz0iMjAuMTgsMTkuODMgMjAuNjQsLTguNDUgMjEuNSwtOC40MSAiLz4KICAgIDxwb2x5Z29uIGlkPSI2NiIgY2xhc3M9ImZpbDY2IiBwb2ludHM9IjIwLjE4LDE5LjgzIDIxLjMzLC04LjQyIDIyLjIsLTguMzUgIi8+CiAgICA8cG9seWdvbiBpZD0iNjciIGNsYXNzPSJmaWw2NyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyMi4wMiwtOC4zNyAyMi44OSwtOC4yOCAiLz4KICAgIDxwb2x5Z29uIGlkPSI2OCIgY2xhc3M9ImZpbDY4IiBwb2ludHM9IjIwLjE4LDE5LjgzIDIyLjcyLC04LjMgMjMuNTgsLTguMiAiLz4KICAgIDxwb2x5Z29uIGlkPSI2OSIgY2xhc3M9ImZpbDY5IiBwb2ludHM9IjIwLjE4LDE5LjgzIDIzLjQxLC04LjIyIDI0LjI3LC04LjA5ICIvPgogICAgPHBvbHlnb24gaWQ9IjcwIiBjbGFzcz0iZmlsNzAiIHBvaW50cz0iMjAuMTgsMTkuODMgMjQuMSwtOC4xMiAyNC45NSwtNy45NyAiLz4KICAgIDxwb2x5Z29uIGlkPSI3MSIgY2xhc3M9ImZpbDcxIiBwb2ludHM9IjIwLjE4LDE5LjgzIDI0Ljc4LC04IDI1LjY0LC03LjgzICIvPgogICAgPHBvbHlnb24gaWQ9IjcyIiBjbGFzcz0iZmlsNzIiIHBvaW50cz0iMjAuMTgsMTkuODMgMjUuNDcsLTcuODYgMjYuMzIsLTcuNjggIi8+CiAgICA8cG9seWdvbiBpZD0iNzMiIGNsYXNzPSJmaWw3MyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyNi4xNSwtNy43MSAyNi45OSwtNy41ICIvPgogICAgPHBvbHlnb24gaWQ9Ijc0IiBjbGFzcz0iZmlsNzQiIHBvaW50cz0iMjAuMTgsMTkuODMgMjYuODIsLTcuNTUgMjcuNjcsLTcuMzIgIi8+CiAgICA8cG9seWdvbiBpZD0iNzUiIGNsYXNzPSJmaWw3NSIgcG9pbnRzPSIyMC4xOCwxOS44MyAyNy41LC03LjM2IDI4LjMzLC03LjExICIvPgogICAgPHBvbHlnb24gaWQ9Ijc2IiBjbGFzcz0iZmlsNzYiIHBvaW50cz0iMjAuMTgsMTkuODMgMjguMTcsLTcuMTYgMjksLTYuODkgIi8+CiAgICA8cG9seWdvbiBpZD0iNzciIGNsYXNzPSJmaWw3NyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyOC44MywtNi45NSAyOS42NSwtNi42NSAiLz4KICAgIDxwb2x5Z29uIGlkPSI3OCIgY2xhc3M9ImZpbDc4IiBwb2ludHM9IjIwLjE4LDE5LjgzIDI5LjQ5LC02LjcxIDMwLjMsLTYuNCAiLz4KICAgIDxwb2x5Z29uIGlkPSI3OSIgY2xhc3M9ImZpbDc5IiBwb2ludHM9IjIwLjE4LDE5LjgzIDMwLjE0LC02LjQ2IDMwLjk1LC02LjEzICIvPgogICAgPHBvbHlnb24gaWQ9IjgwIiBjbGFzcz0iZmlsODAiIHBvaW50cz0iMjAuMTgsMTkuODMgMzAuNzksLTYuMiAzMS41OSwtNS44NSAiLz4KICAgIDxwb2x5Z29uIGlkPSI4MSIgY2xhc3M9ImZpbDgxIiBwb2ludHM9IjIwLjE4LDE5LjgzIDMxLjQzLC01LjkyIDMyLjIyLC01LjU1ICIvPgogICAgPHBvbHlnb24gaWQ9IjgyIiBjbGFzcz0iZmlsODIiIHBvaW50cz0iMjAuMTgsMTkuODMgMzIuMDYsLTUuNjIgMzIuODUsLTUuMjQgIi8+CiAgICA8cG9seWdvbiBpZD0iODMiIGNsYXNzPSJmaWw4MyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzMi42OSwtNS4zMSAzMy40NiwtNC45MSAiLz4KICAgIDxwb2x5Z29uIGlkPSI4NCIgY2xhc3M9ImZpbDg0IiBwb2ludHM9IjIwLjE4LDE5LjgzIDMzLjMxLC00Ljk5IDM0LjA3LC00LjU2ICIvPgogICAgPHBvbHlnb24gaWQ9Ijg1IiBjbGFzcz0iZmlsODUiIHBvaW50cz0iMjAuMTgsMTkuODMgMzMuOTIsLTQuNjUgMzQuNjcsLTQuMiAiLz4KICAgIDxwb2x5Z29uIGlkPSI4NiIgY2xhc3M9ImZpbDg2IiBwb2ludHM9IjIwLjE4LDE5LjgzIDM0LjUyLC00LjI5IDM1LjI3LC0zLjgzICIvPgogICAgPHBvbHlnb24gaWQ9Ijg3IiBjbGFzcz0iZmlsODciIHBvaW50cz0iMjAuMTgsMTkuODMgMzUuMTIsLTMuOTIgMzUuODUsLTMuNDQgIi8+CiAgICA8cG9seWdvbiBpZD0iODgiIGNsYXNzPSJmaWw4OCIgcG9pbnRzPSIyMC4xOCwxOS44MyAzNS43LC0zLjU0IDM2LjQyLC0zLjA0ICIvPgogICAgPHBvbHlnb24gaWQ9Ijg5IiBjbGFzcz0iZmlsODkiIHBvaW50cz0iMjAuMTgsMTkuODMgMzYuMjgsLTMuMTQgMzYuOTksLTIuNjIgIi8+CiAgICA8cG9seWdvbiBpZD0iOTAiIGNsYXNzPSJmaWw5MCIgcG9pbnRzPSIyMC4xOCwxOS44MyAzNi44NSwtMi43MiAzNy41NCwtMi4xOSAiLz4KICAgIDxwb2x5Z29uIGlkPSI5MSIgY2xhc3M9ImZpbDkxIiBwb2ludHM9IjIwLjE4LDE5LjgzIDM3LjQsLTIuMyAzOC4wOCwtMS43NSAiLz4KICAgIDxwb2x5Z29uIGlkPSI5MiIgY2xhc3M9ImZpbDkyIiBwb2ludHM9IjIwLjE4LDE5LjgzIDM3Ljk1LC0xLjg2IDM4LjYyLC0xLjI5ICIvPgogICAgPHBvbHlnb24gaWQ9IjkzIiBjbGFzcz0iZmlsOTMiIHBvaW50cz0iMjAuMTgsMTkuODMgMzguNDgsLTEuNDEgMzkuMTQsLTAuODIgIi8+CiAgICA8cG9seWdvbiBpZD0iOTQiIGNsYXNzPSJmaWw5NCIgcG9pbnRzPSIyMC4xOCwxOS44MyAzOS4wMSwtMC45NCAzOS42NSwtMC4zNCAiLz4KICAgIDxwb2x5Z29uIGlkPSI5NSIgY2xhc3M9ImZpbDk1IiBwb2ludHM9IjIwLjE4LDE5LjgzIDM5LjUyLC0wLjQ2IDQwLjE1LDAuMTUgIi8+CiAgICA8cG9seWdvbiBpZD0iOTYiIGNsYXNzPSJmaWw5NiIgcG9pbnRzPSIyMC4xOCwxOS44MyA0MC4wMiwwLjAzIDQwLjYzLDAuNjUgIi8+CiAgICA8cG9seWdvbiBpZD0iOTciIGNsYXNzPSJmaWw5NyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0MC41MSwwLjUzIDQxLjExLDEuMTcgIi8+CiAgICA8cG9seWdvbiBpZD0iOTgiIGNsYXNzPSJmaWw5OCIgcG9pbnRzPSIyMC4xOCwxOS44MyA0MC45OSwxLjA0IDQxLjU3LDEuNyAiLz4KICAgIDxwb2x5Z29uIGlkPSI5OSIgY2xhc3M9ImZpbDk5IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQxLjQ1LDEuNTcgNDIuMDIsMi4yNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDAiIGNsYXNzPSJmaWwxMDAiIHBvaW50cz0iMjAuMTgsMTkuODMgNDEuOSwyLjEgNDIuNDUsMi43OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDEiIGNsYXNzPSJmaWwxMDEiIHBvaW50cz0iMjAuMTgsMTkuODMgNDIuMzQsMi42NSA0Mi44NywzLjM1ICIvPgogICAgPHBvbHlnb24gaWQ9IjEwMiIgY2xhc3M9ImZpbDEwMiIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Mi43NywzLjIxIDQzLjI4LDMuOTIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTAzIiBjbGFzcz0iZmlsMTAzIiBwb2ludHM9IjIwLjE4LDE5LjgzIDQzLjE4LDMuNzcgNDMuNjgsNC40OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDQiIGNsYXNzPSJmaWwxMDQiIHBvaW50cz0iMjAuMTgsMTkuODMgNDMuNTgsNC4zNSA0NC4wNiw1LjA4ICIvPgogICAgPHBvbHlnb24gaWQ9IjEwNSIgY2xhc3M9ImZpbDEwNSIgcG9pbnRzPSIyMC4xOCwxOS44MyA0My45Niw0Ljk0IDQ0LjQyLDUuNjggIi8+CiAgICA8cG9seWdvbiBpZD0iMTA2IiBjbGFzcz0iZmlsMTA2IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ0LjMzLDUuNTMgNDQuNzcsNi4yOSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDciIGNsYXNzPSJmaWwxMDciIHBvaW50cz0iMjAuMTgsMTkuODMgNDQuNjgsNi4xMyA0NS4xMSw2LjkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTA4IiBjbGFzcz0iZmlsMTA4IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ1LjAyLDYuNzUgNDUuNDMsNy41MiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDkiIGNsYXNzPSJmaWwxMDkiIHBvaW50cz0iMjAuMTgsMTkuODMgNDUuMzUsNy4zNyA0NS43NCw4LjE1ICIvPgogICAgPHBvbHlnb24gaWQ9IjExMCIgY2xhc3M9ImZpbDExMCIgcG9pbnRzPSIyMC4xOCwxOS44MyA0NS42Niw3Ljk5IDQ2LjAzLDguNzkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTExIiBjbGFzcz0iZmlsMTExIiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ1Ljk1LDguNjMgNDYuMyw5LjQzICIvPgogICAgPHBvbHlnb24gaWQ9IjExMiIgY2xhc3M9ImZpbDExMiIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ni4yMyw5LjI3IDQ2LjU2LDEwLjA4ICIvPgogICAgPHBvbHlnb24gaWQ9IjExMyIgY2xhc3M9ImZpbDExMyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ni41LDkuOTIgNDYuODEsMTAuNzMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTE0IiBjbGFzcz0iZmlsMTE0IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ2Ljc0LDEwLjU3IDQ3LjAzLDExLjM5ICIvPgogICAgPHBvbHlnb24gaWQ9IjExNSIgY2xhc3M9ImZpbDExNSIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ni45OCwxMS4yMyA0Ny4yNCwxMi4wNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMTYiIGNsYXNzPSJmaWwxMTYiIHBvaW50cz0iMjAuMTgsMTkuODMgNDcuMTksMTEuODkgNDcuNDQsMTIuNzMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTE3IiBjbGFzcz0iZmlsMTE3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ3LjM5LDEyLjU2IDQ3LjYyLDEzLjQgIi8+CiAgICA8cG9seWdvbiBpZD0iMTE4IiBjbGFzcz0iZmlsMTE4IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ3LjU3LDEzLjIzIDQ3Ljc4LDE0LjA4ICIvPgogICAgPHBvbHlnb24gaWQ9IjExOSIgY2xhc3M9ImZpbDExOSIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ny43NCwxMy45MSA0Ny45MywxNC43NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjAiIGNsYXNzPSJmaWwxMjAiIHBvaW50cz0iMjAuMTgsMTkuODMgNDcuODksMTQuNTkgNDguMDUsMTUuNDUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTIxIiBjbGFzcz0iZmlsMTIxIiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjAyLDE1LjI4IDQ4LjE3LDE2LjEzICIvPgogICAgPHBvbHlnb24gaWQ9IjEyMiIgY2xhc3M9ImZpbDEyMiIgcG9pbnRzPSIyMC4xOCwxOS44MyA0OC4xNCwxNS45NiA0OC4yNiwxNi44MiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjMiIGNsYXNzPSJmaWwxMjMiIHBvaW50cz0iMjAuMTgsMTkuODMgNDguMjQsMTYuNjUgNDguMzQsMTcuNTIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTI0IiBjbGFzcz0iZmlsMTI0IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjMyLDE3LjM0IDQ4LjQsMTguMjEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTI1IiBjbGFzcz0iZmlsMTI1IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjM4LDE4LjA0IDQ4LjQ1LDE4LjkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTI2IiBjbGFzcz0iZmlsMTI2IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjQzLDE4LjczIDQ4LjQ3LDE5LjYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTI3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjQ2LDE5LjQyIDQ4LjQ4LDIwLjI5ICIvPgogICAgPHBvbHlnb24gaWQ9IjEyOCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0OC40OCwyMC4xMiA0OC40OCwyMC45OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDguNDgsMjAuODEgNDguNDUsMjEuNjggIi8+CiAgICA8cG9seWdvbiBpZD0iMTMwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjQ2LDIxLjUgNDguNDEsMjIuMzcgIi8+CiAgICA8cG9seWdvbiBpZD0iMTMxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjQyLDIyLjIgNDguMzUsMjMuMDYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTMyIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjM3LDIyLjg5IDQ4LjI4LDIzLjc1ICIvPgogICAgPHBvbHlnb24gaWQ9IjEzMyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0OC4zLDIzLjU4IDQ4LjE5LDI0LjQ0ICIvPgogICAgPHBvbHlnb24gaWQ9IjEzNCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0OC4yMSwyNC4yNiA0OC4wOCwyNS4xMiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMzUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDguMSwyNC45NSA0Ny45NSwyNS44ICIvPgogICAgPHBvbHlnb24gaWQ9IjEzNiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ny45OCwyNS42MyA0Ny44MSwyNi40OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMzciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDcuODQsMjYuMzEgNDcuNjUsMjcuMTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTM4IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ3LjY5LDI2Ljk4IDQ3LjQ4LDI3LjgyICIvPgogICAgPHBvbHlnb24gaWQ9IjEzOSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ny41MiwyNy42NSA0Ny4yOCwyOC40OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDAiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDcuMzMsMjguMzIgNDcuMDcsMjkuMTQgIi8+CiAgICA8cG9seWdvbiBpZD0iMTQxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ3LjEzLDI4Ljk4IDQ2Ljg1LDI5Ljc5ICIvPgogICAgPHBvbHlnb24gaWQ9IjE0MiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ni45MSwyOS42MyA0Ni42MSwzMC40NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDYuNjcsMzAuMjggNDYuMzUsMzEuMDggIi8+CiAgICA8cG9seWdvbiBpZD0iMTQ0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ2LjQyLDMwLjkyIDQ2LjA4LDMxLjcyICIvPgogICAgPHBvbHlnb24gaWQ9IjE0NSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ni4xNSwzMS41NiA0NS43OSwzMi4zNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDUuODYsMzIuMTggNDUuNDksMzIuOTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTQ3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ1LjU3LDMyLjgxIDQ1LjE3LDMzLjU3ICIvPgogICAgPHBvbHlnb24gaWQ9IjE0OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0NS4yNSwzMy40MiA0NC44NCwzNC4xNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDQuOTIsMzQuMDIgNDQuNDksMzQuNzcgIi8+CiAgICA8cG9seWdvbiBpZD0iMTUwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ0LjU4LDM0LjYyIDQ0LjEzLDM1LjM1ICIvPgogICAgPHBvbHlnb24gaWQ9IjE1MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0NC4yMiwzNS4yMSA0My43NSwzNS45MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNTIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDMuODQsMzUuNzggNDMuMzYsMzYuNSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNTMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDMuNDYsMzYuMzUgNDIuOTUsMzcuMDUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTU0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQzLjA1LDM2LjkxIDQyLjUzLDM3LjYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTU1IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQyLjY0LDM3LjQ2IDQyLjEsMzguMTMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTU2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQyLjIxLDM4IDQxLjY1LDM4LjY2ICIvPgogICAgPHBvbHlnb24gaWQ9IjE1NyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0MS43NywzOC41MiA0MS4yLDM5LjE3ICIvPgogICAgPHBvbHlnb24gaWQ9IjE1OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0MS4zMSwzOS4wNCA0MC43MiwzOS42NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNTkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDAuODQsMzkuNTQgNDAuMjQsNDAuMTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTYwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQwLjM2LDQwLjA0IDM5Ljc0LDQwLjY0ICIvPgogICAgPHBvbHlnb24gaWQ9IjE2MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzOS44Nyw0MC41MiAzOS4yNCw0MS4xICIvPgogICAgPHBvbHlnb24gaWQ9IjE2MiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzOS4zNiw0MC45OCAzOC43Miw0MS41NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNjMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMzguODUsNDEuNDQgMzguMTksNDEuOTkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTY0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDM4LjMyLDQxLjg4IDM3LjY1LDQyLjQxICIvPgogICAgPHBvbHlnb24gaWQ9IjE2NSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzNy43OCw0Mi4zMSAzNy4wOSw0Mi44MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNjYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMzcuMjMsNDIuNzIgMzYuNTMsNDMuMjIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTY3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDM2LjY3LDQzLjEyIDM1Ljk2LDQzLjYxICIvPgogICAgPHBvbHlnb24gaWQ9IjE2OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzNi4xLDQzLjUxIDM1LjM4LDQzLjk4ICIvPgogICAgPHBvbHlnb24gaWQ9IjE2OSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzNS41Miw0My44OCAzNC43OSw0NC4zMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNzAiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMzQuOTMsNDQuMjQgMzQuMTksNDQuNjcgIi8+CiAgICA8cG9seWdvbiBpZD0iMTcxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDM0LjM0LDQ0LjU4IDMzLjU4LDQ0Ljk5ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3MiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzMy43Myw0NC45MSAzMi45Niw0NS4zICIvPgogICAgPHBvbHlnb24gaWQ9IjE3MyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzMy4xMiw0NS4yMyAzMi4zNCw0NS42ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3NCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzMi41LDQ1LjUyIDMxLjcxLDQ1Ljg4ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3NSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzMS44Nyw0NS44MSAzMS4wNyw0Ni4xNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNzYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMzEuMjMsNDYuMDcgMzAuNDMsNDYuMzkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTc3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDMwLjU5LDQ2LjMyIDI5Ljc4LDQ2LjYyICIvPgogICAgPHBvbHlnb24gaWQ9IjE3OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyOS45NCw0Ni41NiAyOS4xMiw0Ni44MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNzkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMjkuMjksNDYuNzggMjguNDYsNDcuMDMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTgwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDI4LjYyLDQ2Ljk4IDI3Ljc5LDQ3LjIyICIvPgogICAgPHBvbHlnb24gaWQ9IjE4MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyNy45Niw0Ny4xNyAyNy4xMiw0Ny4zOCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMjcuMjksNDcuMzQgMjYuNDUsNDcuNTMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTgzIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDI2LjYxLDQ3LjQ5IDI1Ljc3LDQ3LjY2ICIvPgogICAgPHBvbHlnb24gaWQ9IjE4NCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyNS45NCw0Ny42MyAyNS4wOCw0Ny43OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMjUuMjUsNDcuNzUgMjQuNCw0Ny44OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMjQuNTcsNDcuODUgMjMuNzEsNDcuOTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTg3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDIzLjg4LDQ3Ljk0IDIzLjAyLDQ4LjAzICIvPgogICAgPHBvbHlnb24gaWQ9IjE4OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyMy4xOSw0OC4wMSAyMi4zMyw0OC4wNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMjIuNSw0OC4wNiAyMS42NCw0OC4xICIvPgogICAgPHBvbHlnb24gaWQ9IjE5MCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyMS44MSw0OC4xIDIwLjk0LDQ4LjEyICIvPgogICAgPHBvbHlnb24gaWQ9IjE5MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyMS4xMSw0OC4xMSAyMC4yNSw0OC4xMiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOTIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMjAuNDIsNDguMTIgMTkuNTUsNDguMSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOTMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMTkuNzMsNDguMSAxOC44Niw0OC4wNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOTQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMTkuMDMsNDguMDcgMTguMTYsNDggIi8+CiAgICA8cG9seWdvbiBpZD0iMTk1IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDE4LjM0LDQ4LjAyIDE3LjQ3LDQ3LjkzICIvPgogICAgPHBvbHlnb24gaWQ9IjE5NiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAxNy42NSw0Ny45NSAxNi43OCw0Ny44NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOTciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMTYuOTUsNDcuODcgMTYuMDksNDcuNzQgIi8+CiAgICA8cG9seWdvbiBpZD0iMTk4IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDE2LjI3LDQ3Ljc3IDE1LjQxLDQ3LjYyICIvPgogICAgPHBvbHlnb24gaWQ9IjE5OSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAxNS41OCw0Ny42NSAxNC43Miw0Ny40OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDAiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMTQuOSw0Ny41MSAxNC4wNCw0Ny4zMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDEiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMTQuMjEsNDcuMzYgMTMuMzcsNDcuMTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjAyIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDEzLjU0LDQ3LjIgMTIuNyw0Ni45NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMTIuODYsNDcuMDEgMTIuMDMsNDYuNzYgIi8+CiAgICA8cG9seWdvbiBpZD0iMjA0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDEyLjIsNDYuODEgMTEuMzcsNDYuNTQgIi8+CiAgICA8cG9seWdvbiBpZD0iMjA1IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDExLjUzLDQ2LjYgMTAuNzEsNDYuMzEgIi8+CiAgICA8cG9seWdvbiBpZD0iMjA2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDEwLjg3LDQ2LjM2IDEwLjA2LDQ2LjA1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIwNyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAxMC4yMiw0Ni4xMSA5LjQxLDQ1Ljc4ICIvPgogICAgPHBvbHlnb24gaWQ9IjIwOCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA5LjU3LDQ1Ljg1IDguNzcsNDUuNSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgOC45Myw0NS41NyA4LjE0LDQ1LjIgIi8+CiAgICA8cG9seWdvbiBpZD0iMjEwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDguMyw0NS4yNyA3LjUxLDQ0Ljg5ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxMSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA3LjY3LDQ0Ljk2IDYuOSw0NC41NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMTIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNy4wNSw0NC42NCA2LjI5LDQ0LjIxICIvPgogICAgPHBvbHlnb24gaWQ9IjIxMyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA2LjQ0LDQ0LjMgNS42OSw0My44NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMTQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNS44NCw0My45NCA1LjA5LDQzLjQ4ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxNSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA1LjI0LDQzLjU3IDQuNTEsNDMuMDkgIi8+CiAgICA8cG9seWdvbiBpZD0iMjE2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQuNjYsNDMuMTkgMy45NCw0Mi42OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMTciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNC4wOCw0Mi43OSAzLjM3LDQyLjI3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxOCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzLjUyLDQyLjM3IDIuODIsNDEuODQgIi8+CiAgICA8cG9seWdvbiBpZD0iMjE5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDIuOTYsNDEuOTUgMi4yOCw0MS40ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyMCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyLjQxLDQxLjUxIDEuNzQsNDAuOTQgIi8+CiAgICA8cG9seWdvbiBpZD0iMjIxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDEuODgsNDEuMDYgMS4yMiw0MC40NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMS4zNSw0MC41OSAwLjcxLDM5Ljk5ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyMyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAwLjg0LDQwLjExIDAuMjEsMzkuNSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMC4zNCwzOS42MiAtMC4yNywzOSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTAuMTUsMzkuMTIgLTAuNzUsMzguNDggIi8+CiAgICA8cG9seWdvbiBpZD0iMjI2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC0wLjYzLDM4LjYxIC0xLjIxLDM3Ljk1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyNyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMS4wOSwzOC4wOCAtMS42NiwzNy40MSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTEuNTQsMzcuNTUgLTIuMDksMzYuODYgIi8+CiAgICA8cG9seWdvbiBpZD0iMjI5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC0xLjk4LDM3IC0yLjUxLDM2LjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjMwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC0yLjQxLDM2LjQ0IC0yLjkyLDM1LjczICIvPgogICAgPHBvbHlnb24gaWQ9IjIzMSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMi44MiwzNS44OCAtMy4zMiwzNS4xNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMzIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTMuMjIsMzUuMyAtMy43LDM0LjU3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzMyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMy42LDM0LjcxIC00LjA2LDMzLjk3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzNCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMy45NywzNC4xMiAtNC40MSwzMy4zNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMzUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTQuMzIsMzMuNTIgLTQuNzUsMzIuNzUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjM2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC00LjY2LDMyLjkgLTUuMDcsMzIuMTMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjM3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC00Ljk5LDMyLjI4IC01LjM4LDMxLjUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjM4IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC01LjMsMzEuNjYgLTUuNjcsMzAuODYgIi8+CiAgICA8cG9seWdvbiBpZD0iMjM5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC01LjU5LDMxLjAyIC01Ljk0LDMwLjIyICIvPgogICAgPHBvbHlnb24gaWQ9IjI0MCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNS44NywzMC4zOCAtNi4yLDI5LjU3ICIvPgogICAgPHBvbHlnb24gaWQ9IjI0MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNi4xNCwyOS43MyAtNi40NCwyOC45MiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTYuMzgsMjkuMDggLTYuNjcsMjguMjYgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQzIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC02LjYxLDI4LjQyIC02Ljg4LDI3LjU5ICIvPgogICAgPHBvbHlnb24gaWQ9IjI0NCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNi44MywyNy43NiAtNy4wOCwyNi45MiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuMDMsMjcuMDkgLTcuMjYsMjYuMjUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQ2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC03LjIxLDI2LjQyIC03LjQyLDI1LjU3ICIvPgogICAgPHBvbHlnb24gaWQ9IjI0NyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNy4zOCwyNS43NCAtNy41NiwyNC44OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuNTMsMjUuMDYgLTcuNjksMjQuMiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuNjYsMjQuMzcgLTcuODEsMjMuNTIgIi8+CiAgICA8cG9seWdvbiBpZD0iMjUwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC03Ljc4LDIzLjY5IC03LjksMjIuODMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjUxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC03Ljg4LDIzIC03Ljk4LDIyLjE0ICIvPgogICAgPHBvbHlnb24gaWQ9IjI1MiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNy45NiwyMi4zMSAtOC4wNCwyMS40NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNTMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTguMDIsMjEuNjIgLTguMDgsMjAuNzUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjU0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC04LjA3LDIwLjkyIC04LjExLDIwLjA1ICIvPgogICAgPHBvbHlnb24gaWQ9IjI1NSIgY2xhc3M9ImZpbDEyOCIgcG9pbnRzPSIyMC4xOCwxOS44MyAtOC4xLDIwLjIzIC04LjEyLDE5LjUzICIvPgogICA8L2c+CiAgPC9nPgogPC9nPgo8L3N2Zz4=") top no-repeat;
}
html.theme-dark .circleWrapper-2qn7A4BC{
	background-image:url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbDpzcGFjZT0icHJlc2VydmUiIHdpZHRoPSIyMjBweCIgaGVpZ2h0PSIxMTBweCIgdmVyc2lvbj0iMS4xIiBzdHlsZT0ic2hhcGUtcmVuZGVyaW5nOmdlb21ldHJpY1ByZWNpc2lvbjsgdGV4dC1yZW5kZXJpbmc6Z2VvbWV0cmljUHJlY2lzaW9uOyBpbWFnZS1yZW5kZXJpbmc6b3B0aW1pemVRdWFsaXR5OyBmaWxsLXJ1bGU6ZXZlbm9kZDsgY2xpcC1ydWxlOmV2ZW5vZGQiCnZpZXdCb3g9IjAgMCAzOS43MyAxOS44NiIKIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIj4KIDxkZWZzPgogIDxzdHlsZSB0eXBlPSJ0ZXh0L2NzcyI+CiAgIDwhW0NEQVRBWwogICAgLmZpbDY0IHtmaWxsOiMwMEIyQzZ9CiAgICAuZmlsNjMge2ZpbGw6IzAwQjJDOH0KICAgIC5maWw2NyB7ZmlsbDojMDBCM0MwfQogICAgLmZpbDY2IHtmaWxsOiMwMEIzQzJ9CiAgICAuZmlsNjUge2ZpbGw6IzAwQjNDNH0KICAgIC5maWw3MCB7ZmlsbDojMDBCNEJCfQogICAgLmZpbDY5IHtmaWxsOiMwMEI0QkR9CiAgICAuZmlsNjgge2ZpbGw6IzAwQjRCRn0KICAgIC5maWw3MyB7ZmlsbDojMDBCNUI2fQogICAgLmZpbDcyIHtmaWxsOiMwMEI1Qjh9CiAgICAuZmlsNzEge2ZpbGw6IzAwQjVCOX0KICAgIC5maWw3NiB7ZmlsbDojMDBCNkIxfQogICAgLmZpbDc1IHtmaWxsOiMwMEI2QjJ9CiAgICAuZmlsNzQge2ZpbGw6IzAwQjZCNH0KICAgIC5maWw3OSB7ZmlsbDojMDBCN0FCfQogICAgLmZpbDc4IHtmaWxsOiMwMEI3QUR9CiAgICAuZmlsNzcge2ZpbGw6IzAwQjdBRn0KICAgIC5maWw4MiB7ZmlsbDojMDBCOEE2fQogICAgLmZpbDgxIHtmaWxsOiMwMEI4QTh9CiAgICAuZmlsODAge2ZpbGw6IzAwQjhBOX0KICAgIC5maWw4NSB7ZmlsbDojMDBCOUExfQogICAgLmZpbDg0IHtmaWxsOiMwMEI5QTJ9CiAgICAuZmlsODMge2ZpbGw6IzAwQjlBNH0KICAgIC5maWw4OCB7ZmlsbDojMDBCQTlCfQogICAgLmZpbDg3IHtmaWxsOiMwMEJBOUR9CiAgICAuZmlsODYge2ZpbGw6IzAwQkE5Rn0KICAgIC5maWw5MSB7ZmlsbDojMDBCQjk2fQogICAgLmZpbDkwIHtmaWxsOiMwMEJCOTh9CiAgICAuZmlsODkge2ZpbGw6IzAwQkI5OX0KICAgIC5maWw5NCB7ZmlsbDojMDBCQzkxfQogICAgLmZpbDkzIHtmaWxsOiMwMEJDOTJ9CiAgICAuZmlsOTIge2ZpbGw6IzAwQkM5NH0KICAgIC5maWw5NyB7ZmlsbDojMDBCRDhCfQogICAgLmZpbDk2IHtmaWxsOiMwMEJEOER9CiAgICAuZmlsOTUge2ZpbGw6IzAwQkQ4Rn0KICAgIC5maWwxMDAge2ZpbGw6IzAwQkU4Nn0KICAgIC5maWw5OSB7ZmlsbDojMDBCRTg4fQogICAgLmZpbDk4IHtmaWxsOiMwMEJFOEF9CiAgICAuZmlsMTAzIHtmaWxsOiMwMEJGODF9CiAgICAuZmlsMTAyIHtmaWxsOiMwMEJGODJ9CiAgICAuZmlsMTAxIHtmaWxsOiMwMEJGODR9CiAgICAuZmlsMTA2IHtmaWxsOiMwMEMwN0J9CiAgICAuZmlsMTA1IHtmaWxsOiMwMEMwN0R9CiAgICAuZmlsMTA0IHtmaWxsOiMwMEMwN0Z9CiAgICAuZmlsMTA5IHtmaWxsOiMwMEMxNzZ9CiAgICAuZmlsMTA4IHtmaWxsOiMwMEMxNzh9CiAgICAuZmlsMTA3IHtmaWxsOiMwMEMxN0F9CiAgICAuZmlsMTEyIHtmaWxsOiMwMEMyNzF9CiAgICAuZmlsMTExIHtmaWxsOiMwMEMyNzJ9CiAgICAuZmlsMTEwIHtmaWxsOiMwMEMyNzR9CiAgICAuZmlsMTE1IHtmaWxsOiMwMEMzNkJ9CiAgICAuZmlsMTE0IHtmaWxsOiMwMEMzNkR9CiAgICAuZmlsMTEzIHtmaWxsOiMwMEMzNkZ9CiAgICAuZmlsMTE4IHtmaWxsOiMwMEM0NjZ9CiAgICAuZmlsMTE3IHtmaWxsOiMwMEM0Njh9CiAgICAuZmlsMTE2IHtmaWxsOiMwMEM0NkF9CiAgICAuZmlsMTIxIHtmaWxsOiMwMEM1NjF9CiAgICAuZmlsMTIwIHtmaWxsOiMwMEM1NjN9CiAgICAuZmlsMTE5IHtmaWxsOiMwMEM1NjR9CiAgICAuZmlsMTI0IHtmaWxsOiMwMEM2NUJ9CiAgICAuZmlsMTIzIHtmaWxsOiMwMEM2NUR9CiAgICAuZmlsMTIyIHtmaWxsOiMwMEM2NUZ9CiAgICAuZmlsMTI3IHtmaWxsOiMwMEM3NTd9CiAgICAuZmlsMTI2IHtmaWxsOiMwMEM3NTh9CiAgICAuZmlsMTI1IHtmaWxsOiMwMEM3NUF9CiAgICAuZmlsNjIge2ZpbGw6IzAzQjBDNn0KICAgIC5maWw2MSB7ZmlsbDojMDdBREM0fQogICAgLmZpbDYwIHtmaWxsOiMwQkFBQzJ9CiAgICAuZmlsNTkge2ZpbGw6IzBGQThDMH0KICAgIC5maWw1OCB7ZmlsbDojMTNBNUJFfQogICAgLmZpbDU3IHtmaWxsOiMxN0EyQkN9CiAgICAuZmlsNTYge2ZpbGw6IzFCOUZCQX0KICAgIC5maWw1NSB7ZmlsbDojMUY5Q0I3fQogICAgLmZpbDU0IHtmaWxsOiMyMzlBQjV9CiAgICAuZmlsNTMge2ZpbGw6IzI3OTdCM30KICAgIC5maWw1MiB7ZmlsbDojMkI5NEIxfQogICAgLmZpbDUxIHtmaWxsOiMyRjkxQUZ9CiAgICAuZmlsNTAge2ZpbGw6IzMzOEVBRH0KICAgIC5maWw0OSB7ZmlsbDojMzc4Q0FCfQogICAgLmZpbDQ4IHtmaWxsOiMzQjg5QTl9CiAgICAuZmlsNDcge2ZpbGw6IzNGODZBNn0KICAgIC5maWw0NiB7ZmlsbDojNDM4M0E0fQogICAgLmZpbDQ1IHtmaWxsOiM0NzgwQTJ9CiAgICAuZmlsNDQge2ZpbGw6IzRCN0VBMH0KICAgIC5maWw0MyB7ZmlsbDojNEY3QjlFfQogICAgLmZpbDQyIHtmaWxsOiM1Mzc4OUN9CiAgICAuZmlsNDEge2ZpbGw6IzU3NzU5QX0KICAgIC5maWw0MCB7ZmlsbDojNUI3Mjk3fQogICAgLmZpbDM5IHtmaWxsOiM1RjcwOTV9CiAgICAuZmlsMzgge2ZpbGw6IzYzNkQ5M30KICAgIC5maWwzNyB7ZmlsbDojNjc2QTkxfQogICAgLmZpbDM2IHtmaWxsOiM2QjY3OEZ9CiAgICAuZmlsMzUge2ZpbGw6IzZGNjU4RH0KICAgIC5maWwzNCB7ZmlsbDojNzM2MjhCfQogICAgLmZpbDMzIHtmaWxsOiM3NzVGODl9CiAgICAuZmlsMzIge2ZpbGw6IzdCNUM4Nn0KICAgIC5maWwzMSB7ZmlsbDojN0Y1OTg0fQogICAgLmZpbDMwIHtmaWxsOiM4MzU3ODJ9CiAgICAuZmlsMjkge2ZpbGw6Izg3NTQ4MH0KICAgIC5maWwyOCB7ZmlsbDojOEI1MTdFfQogICAgLmZpbDI3IHtmaWxsOiM4RjRFN0N9CiAgICAuZmlsMjYge2ZpbGw6IzkzNEI3QX0KICAgIC5maWwyNSB7ZmlsbDojOTc0OTc3fQogICAgLmZpbDI0IHtmaWxsOiM5QjQ2NzV9CiAgICAuZmlsMjMge2ZpbGw6IzlGNDM3M30KICAgIC5maWwyMiB7ZmlsbDojQTM0MDcxfQogICAgLmZpbDIxIHtmaWxsOiNBNzNENkZ9CiAgICAuZmlsMjAge2ZpbGw6I0FCM0I2RH0KICAgIC5maWwxOSB7ZmlsbDojQUYzODZCfQogICAgLmZpbDE4IHtmaWxsOiNCMzM1Njl9CiAgICAuZmlsMTcge2ZpbGw6I0I3MzI2Nn0KICAgIC5maWwxNiB7ZmlsbDojQkIyRjY0fQogICAgLmZpbDE1IHtmaWxsOiNCRjJENjJ9CiAgICAuZmlsMTQge2ZpbGw6I0MzMkE2MH0KICAgIC5maWwxMyB7ZmlsbDojQzcyNzVFfQogICAgLmZpbDEyIHtmaWxsOiNDQjI0NUN9CiAgICAuZmlsMTEge2ZpbGw6I0NGMjI1QX0KICAgIC5maWwxMCB7ZmlsbDojRDMxRjU3fQogICAgLmZpbDkge2ZpbGw6I0Q3MUM1NX0KICAgIC5maWw4IHtmaWxsOiNEQjE5NTN9CiAgICAuZmlsNyB7ZmlsbDojREYxNjUxfQogICAgLmZpbDYge2ZpbGw6I0UzMTQ0Rn0KICAgIC5maWw1IHtmaWxsOiNFNzExNER9CiAgICAuZmlsNCB7ZmlsbDojRUIwRTRCfQogICAgLmZpbDMge2ZpbGw6I0VGMEI0OX0KICAgIC5maWwyIHtmaWxsOiNGMzA4NDZ9CiAgICAuZmlsMSB7ZmlsbDojRjcwNjQ0fQogICAgLmZpbDAge2ZpbGw6I0ZCMDM0Mn0KICAgIC5maWwxMjgge2ZpbGw6I0ZGMDA0MH0KICAgXV0+CiAgPC9zdHlsZT4KICAgIDxjbGlwUGF0aCBpZD0iaWQwIj4KICAgICA8cGF0aCBkPSJNMy41IDguNmMwLjA1LC0wLjA3IDAuMTIsLTAuMTEgMC4yLC0wLjExIDAuMDYsMCAwLjExLDAuMDIgMC4xNSwwLjA1IDAuMTEsMC4wOCAwLjE0LDAuMjQgMC4wNiwwLjM1IC0yLjE3LDMuMTUgLTMuMzYsNi44OSAtMy40MSwxMC43MiAwLDAuMTQgLTAuMTEsMC4yNSAtMC4yNSwwLjI1IC0wLjE0LDAgLTAuMjUsLTAuMTEgLTAuMjUsLTAuMjUgMCwwIDAsMCAwLDAgMC4wNSwtNC4wOCAxLjM0LC03Ljg3IDMuNSwtMTEuMDFsMCAwem0zMi4zOCAtMC4wNmMtMC4wNywwLjA1IC0wLjExLDAuMTMgLTAuMTEsMC4yMSAwLDAuMDUgMC4wMiwwLjEgMC4wNSwwLjE0IDIuMTcsMy4xNSAzLjM2LDYuODkgMy40LDEwLjcyIDAsMC4xNCAwLjEyLDAuMjUgMC4yNiwwLjI1IDAuMTQsMCAwLjI1LC0wLjExIDAuMjUsLTAuMjUgMCwwIDAsMCAwLDAgLTAuMDQsLTMuOTMgLTEuMjcsLTcuNzcgLTMuNSwtMTEuMDEgLTAuMDUsLTAuMDcgLTAuMTIsLTAuMTEgLTAuMjEsLTAuMTEgLTAuMDUsMCAtMC4xLDAuMDIgLTAuMTQsMC4wNWwwIDB6bS05LjQ5IC02LjkxYy0wLjExLC0wLjA0IC0wLjE3LC0wLjEzIC0wLjE3LC0wLjI0IDAsLTAuMDMgMCwtMC4wNSAwLjAxLC0wLjA4IDAuMDMsLTAuMSAwLjEzLC0wLjE3IDAuMjQsLTAuMTcgMC4wMiwwIDAuMDUsMCAwLjA4LDAuMDEgMy42LDEuMjkgNi43NiwzLjYgOS4wOCw2LjYzIDAuMDksMC4xMSAwLjA2LDAuMjcgLTAuMDUsMC4zNSAtMC4wNCwwLjA0IC0wLjEsMC4wNSAtMC4xNSwwLjA1IC0wLjA4LDAgLTAuMTUsLTAuMDMgLTAuMiwtMC4xIC0yLjI3LC0yLjk1IC01LjM0LC01LjE5IC04Ljg0LC02LjQ1bDAgMHptLTEyLjQyIC0wLjQ4YzAuMDQsMC4xMSAwLjE0LDAuMTggMC4yNSwwLjE4IDAuMDIsMCAwLjA1LC0wLjAxIDAuMDcsLTAuMDEgMS44LC0wLjU0IDMuNjcsLTAuODIgNS41NiwtMC44MiAwLDAgMC4wMSwwIDAuMDEsMCAxLjk0LDAgMy44MSwwLjI5IDUuNTgsMC44MiAwLjAyLDAgMC4wNSwwLjAxIDAuMDcsMC4wMSAwLjExLDAgMC4yMSwtMC4wNyAwLjI0LC0wLjE4IDAuMDEsLTAuMDIgMC4wMSwtMC4wNSAwLjAxLC0wLjA3IDAsLTAuMTEgLTAuMDcsLTAuMjEgLTAuMTcsLTAuMjQgLTEuODUsLTAuNTYgLTMuNzgsLTAuODQgLTUuNzEsLTAuODQgMCwwIC0wLjAxLDAgLTAuMDIsMCAtMS45OSwwIC0zLjkxLDAuMjkgLTUuNzIsMC44NCAtMC4xMSwwLjAzIC0wLjE4LDAuMTMgLTAuMTgsMC4yNCAwLDAuMDIgMC4wMSwwLjA1IDAuMDIsMC4wN2wtMC4wMSAwem0tMC40NyAwLjE2YzAuMDEsMC4wMyAwLjAxLDAuMDUgMC4wMSwwLjA4IDAsMC4xMSAtMC4wNywwLjIgLTAuMTcsMC4yNCAtMy41LDEuMjUgLTYuNTgsMy41IC04Ljg0LDYuNDUgLTAuMDUsMC4wNyAtMC4xMiwwLjEgLTAuMiwwLjEgLTAuMDYsMCAtMC4xMSwtMC4wMSAtMC4xNSwtMC4wNSAtMC4wNywtMC4wNCAtMC4xLC0wLjEyIC0wLjEsLTAuMiAwLC0wLjA1IDAuMDEsLTAuMSAwLjA1LC0wLjE1IDIuMzIsLTMuMDMgNS40OCwtNS4zNCA5LjA4LC02LjYzIDAuMTMsLTAuMDQgMC4yNywwLjAzIDAuMzIsMC4xNmwwIDB6Ii8+CiAgICA8L2NsaXBQYXRoPgogPC9kZWZzPgogPGcgaWQ9IjEiPgogIDxnPgogICA8ZyBzdHlsZT0iY2xpcC1wYXRoOnVybCgjaWQwKSI+CiAgICA8cG9seWdvbiBjbGFzcz0iZmlsMCIgcG9pbnRzPSIyMC4xOCwxOS44MyAtOC4xMiwxOS43MSAtOC4xMSwxOC42NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxIiBjbGFzcz0iZmlsMSIgcG9pbnRzPSIyMC4xOCwxOS44MyAtOC4xMiwxOC44NCAtOC4wOSwxNy45NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyIiBjbGFzcz0iZmlsMiIgcG9pbnRzPSIyMC4xOCwxOS44MyAtOC4xLDE4LjE1IC04LjA1LDE3LjI4ICIvPgogICAgPHBvbHlnb24gaWQ9IjMiIGNsYXNzPSJmaWwzIiBwb2ludHM9IjIwLjE4LDE5LjgzIC04LjA2LDE3LjQ1IC03Ljk5LDE2LjU5ICIvPgogICAgPHBvbHlnb24gaWQ9IjQiIGNsYXNzPSJmaWw0IiBwb2ludHM9IjIwLjE4LDE5LjgzIC04LjAxLDE2Ljc2IC03LjkyLDE1LjkgIi8+CiAgICA8cG9seWdvbiBpZD0iNSIgY2xhc3M9ImZpbDUiIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuOTMsMTYuMDcgLTcuODMsMTUuMjEgIi8+CiAgICA8cG9seWdvbiBpZD0iNiIgY2xhc3M9ImZpbDYiIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuODUsMTUuMzkgLTcuNzIsMTQuNTMgIi8+CiAgICA8cG9seWdvbiBpZD0iNyIgY2xhc3M9ImZpbDciIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuNzQsMTQuNyAtNy41OSwxMy44NSAiLz4KICAgIDxwb2x5Z29uIGlkPSI4IiBjbGFzcz0iZmlsOCIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNy42MiwxNC4wMiAtNy40NSwxMy4xNyAiLz4KICAgIDxwb2x5Z29uIGlkPSI5IiBjbGFzcz0iZmlsOSIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNy40OCwxMy4zNCAtNy4yOSwxMi41ICIvPgogICAgPHBvbHlnb24gaWQ9IjEwIiBjbGFzcz0iZmlsMTAiIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuMzMsMTIuNjcgLTcuMTEsMTEuODMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTEiIGNsYXNzPSJmaWwxMSIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNy4xNiwxMiAtNi45MiwxMS4xNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMiIgY2xhc3M9ImZpbDEyIiBwb2ludHM9IjIwLjE4LDE5LjgzIC02Ljk3LDExLjMzIC02LjcxLDEwLjUxICIvPgogICAgPHBvbHlnb24gaWQ9IjEzIiBjbGFzcz0iZmlsMTMiIHBvaW50cz0iMjAuMTgsMTkuODMgLTYuNzcsMTAuNjcgLTYuNDksOS44NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNCIgY2xhc3M9ImZpbDE0IiBwb2ludHM9IjIwLjE4LDE5LjgzIC02LjU0LDEwLjAyIC02LjI1LDkuMjEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTUiIGNsYXNzPSJmaWwxNSIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNi4zMSw5LjM3IC01Ljk5LDguNTcgIi8+CiAgICA8cG9seWdvbiBpZD0iMTYiIGNsYXNzPSJmaWwxNiIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNi4wNiw4LjczIC01LjcyLDcuOTQgIi8+CiAgICA8cG9seWdvbiBpZD0iMTciIGNsYXNzPSJmaWwxNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNS43OSw4LjA5IC01LjQzLDcuMzEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTgiIGNsYXNzPSJmaWwxOCIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNS41LDcuNDcgLTUuMTMsNi42OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOSIgY2xhc3M9ImZpbDE5IiBwb2ludHM9IjIwLjE4LDE5LjgzIC01LjIsNi44NSAtNC44MSw2LjA4ICIvPgogICAgPHBvbHlnb24gaWQ9IjIwIiBjbGFzcz0iZmlsMjAiIHBvaW50cz0iMjAuMTgsMTkuODMgLTQuODksNi4yMyAtNC40OCw1LjQ4ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxIiBjbGFzcz0iZmlsMjEiIHBvaW50cz0iMjAuMTgsMTkuODMgLTQuNTYsNS42MyAtNC4xMyw0Ljg4ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyIiBjbGFzcz0iZmlsMjIiIHBvaW50cz0iMjAuMTgsMTkuODMgLTQuMjIsNS4wMyAtMy43Nyw0LjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjMiIGNsYXNzPSJmaWwyMyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMy44Niw0LjQ0IC0zLjM5LDMuNzIgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQiIGNsYXNzPSJmaWwyNCIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMy40OCwzLjg3IC0zLDMuMTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMjUiIGNsYXNzPSJmaWwyNSIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMy4wOSwzLjMgLTIuNTksMi42ICIvPgogICAgPHBvbHlnb24gaWQ9IjI2IiBjbGFzcz0iZmlsMjYiIHBvaW50cz0iMjAuMTgsMTkuODMgLTIuNjksMi43NCAtMi4xNywyLjA1ICIvPgogICAgPHBvbHlnb24gaWQ9IjI3IiBjbGFzcz0iZmlsMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTIuMjgsMi4xOSAtMS43NCwxLjUyICIvPgogICAgPHBvbHlnb24gaWQ9IjI4IiBjbGFzcz0iZmlsMjgiIHBvaW50cz0iMjAuMTgsMTkuODMgLTEuODUsMS42NSAtMS4yOSwwLjk5ICIvPgogICAgPHBvbHlnb24gaWQ9IjI5IiBjbGFzcz0iZmlsMjkiIHBvaW50cz0iMjAuMTgsMTkuODMgLTEuNCwxLjEzIC0wLjgzLDAuNDggIi8+CiAgICA8cG9seWdvbiBpZD0iMzAiIGNsYXNzPSJmaWwzMCIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMC45NSwwLjYxIC0wLjM2LC0wLjAyICIvPgogICAgPHBvbHlnb24gaWQ9IjMxIiBjbGFzcz0iZmlsMzEiIHBvaW50cz0iMjAuMTgsMTkuODMgLTAuNDgsMC4xMSAwLjEyLC0wLjUxICIvPgogICAgPHBvbHlnb24gaWQ9IjMyIiBjbGFzcz0iZmlsMzIiIHBvaW50cz0iMjAuMTgsMTkuODMgMCwtMC4zOSAwLjYyLC0wLjk4ICIvPgogICAgPHBvbHlnb24gaWQ9IjMzIiBjbGFzcz0iZmlsMzMiIHBvaW50cz0iMjAuMTgsMTkuODMgMC40OSwtMC44NiAxLjEyLC0xLjQ1ICIvPgogICAgPHBvbHlnb24gaWQ9IjM0IiBjbGFzcz0iZmlsMzQiIHBvaW50cz0iMjAuMTgsMTkuODMgMSwtMS4zMyAxLjY0LC0xLjkgIi8+CiAgICA8cG9seWdvbiBpZD0iMzUiIGNsYXNzPSJmaWwzNSIgcG9pbnRzPSIyMC4xOCwxOS44MyAxLjUxLC0xLjc5IDIuMTcsLTIuMzQgIi8+CiAgICA8cG9seWdvbiBpZD0iMzYiIGNsYXNzPSJmaWwzNiIgcG9pbnRzPSIyMC4xOCwxOS44MyAyLjA0LC0yLjIzIDIuNzIsLTIuNzYgIi8+CiAgICA8cG9seWdvbiBpZD0iMzciIGNsYXNzPSJmaWwzNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyLjU4LC0yLjY2IDMuMjcsLTMuMTcgIi8+CiAgICA8cG9seWdvbiBpZD0iMzgiIGNsYXNzPSJmaWwzOCIgcG9pbnRzPSIyMC4xOCwxOS44MyAzLjEzLC0zLjA3IDMuODMsLTMuNTcgIi8+CiAgICA8cG9seWdvbiBpZD0iMzkiIGNsYXNzPSJmaWwzOSIgcG9pbnRzPSIyMC4xOCwxOS44MyAzLjY5LC0zLjQ3IDQuNCwtMy45NiAiLz4KICAgIDxwb2x5Z29uIGlkPSI0MCIgY2xhc3M9ImZpbDQwIiBwb2ludHM9IjIwLjE4LDE5LjgzIDQuMjYsLTMuODYgNC45OCwtNC4zMiAiLz4KICAgIDxwb2x5Z29uIGlkPSI0MSIgY2xhc3M9ImZpbDQxIiBwb2ludHM9IjIwLjE4LDE5LjgzIDQuODQsLTQuMjMgNS41NywtNC42OCAiLz4KICAgIDxwb2x5Z29uIGlkPSI0MiIgY2xhc3M9ImZpbDQyIiBwb2ludHM9IjIwLjE4LDE5LjgzIDUuNDMsLTQuNTkgNi4xNywtNS4wMiAiLz4KICAgIDxwb2x5Z29uIGlkPSI0MyIgY2xhc3M9ImZpbDQzIiBwb2ludHM9IjIwLjE4LDE5LjgzIDYuMDIsLTQuOTMgNi43OCwtNS4zNCAiLz4KICAgIDxwb2x5Z29uIGlkPSI0NCIgY2xhc3M9ImZpbDQ0IiBwb2ludHM9IjIwLjE4LDE5LjgzIDYuNjMsLTUuMjYgNy40LC01LjY1ICIvPgogICAgPHBvbHlnb24gaWQ9IjQ1IiBjbGFzcz0iZmlsNDUiIHBvaW50cz0iMjAuMTgsMTkuODMgNy4yNCwtNS41OCA4LjAyLC01Ljk1ICIvPgogICAgPHBvbHlnb24gaWQ9IjQ2IiBjbGFzcz0iZmlsNDYiIHBvaW50cz0iMjAuMTgsMTkuODMgNy44NiwtNS44NyA4LjY1LC02LjIzICIvPgogICAgPHBvbHlnb24gaWQ9IjQ3IiBjbGFzcz0iZmlsNDciIHBvaW50cz0iMjAuMTgsMTkuODMgOC40OSwtNi4xNiA5LjI5LC02LjQ5ICIvPgogICAgPHBvbHlnb24gaWQ9IjQ4IiBjbGFzcz0iZmlsNDgiIHBvaW50cz0iMjAuMTgsMTkuODMgOS4xMywtNi40MiA5LjkzLC02Ljc0ICIvPgogICAgPHBvbHlnb24gaWQ9IjQ5IiBjbGFzcz0iZmlsNDkiIHBvaW50cz0iMjAuMTgsMTkuODMgOS43NywtNi42NyAxMC41OCwtNi45NyAiLz4KICAgIDxwb2x5Z29uIGlkPSI1MCIgY2xhc3M9ImZpbDUwIiBwb2ludHM9IjIwLjE4LDE5LjgzIDEwLjQyLC02LjkxIDExLjI0LC03LjE4ICIvPgogICAgPHBvbHlnb24gaWQ9IjUxIiBjbGFzcz0iZmlsNTEiIHBvaW50cz0iMjAuMTgsMTkuODMgMTEuMDgsLTcuMTMgMTEuOSwtNy4zOCAiLz4KICAgIDxwb2x5Z29uIGlkPSI1MiIgY2xhc3M9ImZpbDUyIiBwb2ludHM9IjIwLjE4LDE5LjgzIDExLjc0LC03LjMzIDEyLjU3LC03LjU2ICIvPgogICAgPHBvbHlnb24gaWQ9IjUzIiBjbGFzcz0iZmlsNTMiIHBvaW50cz0iMjAuMTgsMTkuODMgMTIuNCwtNy41MiAxMy4yNCwtNy43MyAiLz4KICAgIDxwb2x5Z29uIGlkPSI1NCIgY2xhc3M9ImZpbDU0IiBwb2ludHM9IjIwLjE4LDE5LjgzIDEzLjA3LC03LjY5IDEzLjkxLC03Ljg4ICIvPgogICAgPHBvbHlnb24gaWQ9IjU1IiBjbGFzcz0iZmlsNTUiIHBvaW50cz0iMjAuMTgsMTkuODMgMTMuNzUsLTcuODQgMTQuNTksLTguMDEgIi8+CiAgICA8cG9seWdvbiBpZD0iNTYiIGNsYXNzPSJmaWw1NiIgcG9pbnRzPSIyMC4xOCwxOS44MyAxNC40MiwtNy45OCAxNS4yOCwtOC4xMyAiLz4KICAgIDxwb2x5Z29uIGlkPSI1NyIgY2xhc3M9ImZpbDU3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDE1LjExLC04LjEgMTUuOTYsLTguMjMgIi8+CiAgICA8cG9seWdvbiBpZD0iNTgiIGNsYXNzPSJmaWw1OCIgcG9pbnRzPSIyMC4xOCwxOS44MyAxNS43OSwtOC4yIDE2LjY1LC04LjMxICIvPgogICAgPHBvbHlnb24gaWQ9IjU5IiBjbGFzcz0iZmlsNTkiIHBvaW50cz0iMjAuMTgsMTkuODMgMTYuNDgsLTguMjkgMTcuMzQsLTguMzcgIi8+CiAgICA8cG9seWdvbiBpZD0iNjAiIGNsYXNzPSJmaWw2MCIgcG9pbnRzPSIyMC4xOCwxOS44MyAxNy4xNywtOC4zNiAxOC4wMywtOC40MiAiLz4KICAgIDxwb2x5Z29uIGlkPSI2MSIgY2xhc3M9ImZpbDYxIiBwb2ludHM9IjIwLjE4LDE5LjgzIDE3Ljg2LC04LjQxIDE4LjczLC04LjQ1ICIvPgogICAgPHBvbHlnb24gaWQ9IjYyIiBjbGFzcz0iZmlsNjIiIHBvaW50cz0iMjAuMTgsMTkuODMgMTguNTUsLTguNDUgMTkuNDIsLTguNDcgIi8+CiAgICA8cG9seWdvbiBpZD0iNjMiIGNsYXNzPSJmaWw2MyIgcG9pbnRzPSIyMC4xOCwxOS44MyAxOS4yNSwtOC40NiAyMC4xMSwtOC40NyAiLz4KICAgIDxwb2x5Z29uIGlkPSI2NCIgY2xhc3M9ImZpbDY0IiBwb2ludHM9IjIwLjE4LDE5LjgzIDE5Ljk0LC04LjQ2IDIwLjgxLC04LjQ1ICIvPgogICAgPHBvbHlnb24gaWQ9IjY1IiBjbGFzcz0iZmlsNjUiIHBvaW50cz0iMjAuMTgsMTkuODMgMjAuNjQsLTguNDUgMjEuNSwtOC40MSAiLz4KICAgIDxwb2x5Z29uIGlkPSI2NiIgY2xhc3M9ImZpbDY2IiBwb2ludHM9IjIwLjE4LDE5LjgzIDIxLjMzLC04LjQyIDIyLjIsLTguMzUgIi8+CiAgICA8cG9seWdvbiBpZD0iNjciIGNsYXNzPSJmaWw2NyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyMi4wMiwtOC4zNyAyMi44OSwtOC4yOCAiLz4KICAgIDxwb2x5Z29uIGlkPSI2OCIgY2xhc3M9ImZpbDY4IiBwb2ludHM9IjIwLjE4LDE5LjgzIDIyLjcyLC04LjMgMjMuNTgsLTguMiAiLz4KICAgIDxwb2x5Z29uIGlkPSI2OSIgY2xhc3M9ImZpbDY5IiBwb2ludHM9IjIwLjE4LDE5LjgzIDIzLjQxLC04LjIyIDI0LjI3LC04LjA5ICIvPgogICAgPHBvbHlnb24gaWQ9IjcwIiBjbGFzcz0iZmlsNzAiIHBvaW50cz0iMjAuMTgsMTkuODMgMjQuMSwtOC4xMiAyNC45NSwtNy45NyAiLz4KICAgIDxwb2x5Z29uIGlkPSI3MSIgY2xhc3M9ImZpbDcxIiBwb2ludHM9IjIwLjE4LDE5LjgzIDI0Ljc4LC04IDI1LjY0LC03LjgzICIvPgogICAgPHBvbHlnb24gaWQ9IjcyIiBjbGFzcz0iZmlsNzIiIHBvaW50cz0iMjAuMTgsMTkuODMgMjUuNDcsLTcuODYgMjYuMzIsLTcuNjggIi8+CiAgICA8cG9seWdvbiBpZD0iNzMiIGNsYXNzPSJmaWw3MyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyNi4xNSwtNy43MSAyNi45OSwtNy41ICIvPgogICAgPHBvbHlnb24gaWQ9Ijc0IiBjbGFzcz0iZmlsNzQiIHBvaW50cz0iMjAuMTgsMTkuODMgMjYuODIsLTcuNTUgMjcuNjcsLTcuMzIgIi8+CiAgICA8cG9seWdvbiBpZD0iNzUiIGNsYXNzPSJmaWw3NSIgcG9pbnRzPSIyMC4xOCwxOS44MyAyNy41LC03LjM2IDI4LjMzLC03LjExICIvPgogICAgPHBvbHlnb24gaWQ9Ijc2IiBjbGFzcz0iZmlsNzYiIHBvaW50cz0iMjAuMTgsMTkuODMgMjguMTcsLTcuMTYgMjksLTYuODkgIi8+CiAgICA8cG9seWdvbiBpZD0iNzciIGNsYXNzPSJmaWw3NyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyOC44MywtNi45NSAyOS42NSwtNi42NSAiLz4KICAgIDxwb2x5Z29uIGlkPSI3OCIgY2xhc3M9ImZpbDc4IiBwb2ludHM9IjIwLjE4LDE5LjgzIDI5LjQ5LC02LjcxIDMwLjMsLTYuNCAiLz4KICAgIDxwb2x5Z29uIGlkPSI3OSIgY2xhc3M9ImZpbDc5IiBwb2ludHM9IjIwLjE4LDE5LjgzIDMwLjE0LC02LjQ2IDMwLjk1LC02LjEzICIvPgogICAgPHBvbHlnb24gaWQ9IjgwIiBjbGFzcz0iZmlsODAiIHBvaW50cz0iMjAuMTgsMTkuODMgMzAuNzksLTYuMiAzMS41OSwtNS44NSAiLz4KICAgIDxwb2x5Z29uIGlkPSI4MSIgY2xhc3M9ImZpbDgxIiBwb2ludHM9IjIwLjE4LDE5LjgzIDMxLjQzLC01LjkyIDMyLjIyLC01LjU1ICIvPgogICAgPHBvbHlnb24gaWQ9IjgyIiBjbGFzcz0iZmlsODIiIHBvaW50cz0iMjAuMTgsMTkuODMgMzIuMDYsLTUuNjIgMzIuODUsLTUuMjQgIi8+CiAgICA8cG9seWdvbiBpZD0iODMiIGNsYXNzPSJmaWw4MyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzMi42OSwtNS4zMSAzMy40NiwtNC45MSAiLz4KICAgIDxwb2x5Z29uIGlkPSI4NCIgY2xhc3M9ImZpbDg0IiBwb2ludHM9IjIwLjE4LDE5LjgzIDMzLjMxLC00Ljk5IDM0LjA3LC00LjU2ICIvPgogICAgPHBvbHlnb24gaWQ9Ijg1IiBjbGFzcz0iZmlsODUiIHBvaW50cz0iMjAuMTgsMTkuODMgMzMuOTIsLTQuNjUgMzQuNjcsLTQuMiAiLz4KICAgIDxwb2x5Z29uIGlkPSI4NiIgY2xhc3M9ImZpbDg2IiBwb2ludHM9IjIwLjE4LDE5LjgzIDM0LjUyLC00LjI5IDM1LjI3LC0zLjgzICIvPgogICAgPHBvbHlnb24gaWQ9Ijg3IiBjbGFzcz0iZmlsODciIHBvaW50cz0iMjAuMTgsMTkuODMgMzUuMTIsLTMuOTIgMzUuODUsLTMuNDQgIi8+CiAgICA8cG9seWdvbiBpZD0iODgiIGNsYXNzPSJmaWw4OCIgcG9pbnRzPSIyMC4xOCwxOS44MyAzNS43LC0zLjU0IDM2LjQyLC0zLjA0ICIvPgogICAgPHBvbHlnb24gaWQ9Ijg5IiBjbGFzcz0iZmlsODkiIHBvaW50cz0iMjAuMTgsMTkuODMgMzYuMjgsLTMuMTQgMzYuOTksLTIuNjIgIi8+CiAgICA8cG9seWdvbiBpZD0iOTAiIGNsYXNzPSJmaWw5MCIgcG9pbnRzPSIyMC4xOCwxOS44MyAzNi44NSwtMi43MiAzNy41NCwtMi4xOSAiLz4KICAgIDxwb2x5Z29uIGlkPSI5MSIgY2xhc3M9ImZpbDkxIiBwb2ludHM9IjIwLjE4LDE5LjgzIDM3LjQsLTIuMyAzOC4wOCwtMS43NSAiLz4KICAgIDxwb2x5Z29uIGlkPSI5MiIgY2xhc3M9ImZpbDkyIiBwb2ludHM9IjIwLjE4LDE5LjgzIDM3Ljk1LC0xLjg2IDM4LjYyLC0xLjI5ICIvPgogICAgPHBvbHlnb24gaWQ9IjkzIiBjbGFzcz0iZmlsOTMiIHBvaW50cz0iMjAuMTgsMTkuODMgMzguNDgsLTEuNDEgMzkuMTQsLTAuODIgIi8+CiAgICA8cG9seWdvbiBpZD0iOTQiIGNsYXNzPSJmaWw5NCIgcG9pbnRzPSIyMC4xOCwxOS44MyAzOS4wMSwtMC45NCAzOS42NSwtMC4zNCAiLz4KICAgIDxwb2x5Z29uIGlkPSI5NSIgY2xhc3M9ImZpbDk1IiBwb2ludHM9IjIwLjE4LDE5LjgzIDM5LjUyLC0wLjQ2IDQwLjE1LDAuMTUgIi8+CiAgICA8cG9seWdvbiBpZD0iOTYiIGNsYXNzPSJmaWw5NiIgcG9pbnRzPSIyMC4xOCwxOS44MyA0MC4wMiwwLjAzIDQwLjYzLDAuNjUgIi8+CiAgICA8cG9seWdvbiBpZD0iOTciIGNsYXNzPSJmaWw5NyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0MC41MSwwLjUzIDQxLjExLDEuMTcgIi8+CiAgICA8cG9seWdvbiBpZD0iOTgiIGNsYXNzPSJmaWw5OCIgcG9pbnRzPSIyMC4xOCwxOS44MyA0MC45OSwxLjA0IDQxLjU3LDEuNyAiLz4KICAgIDxwb2x5Z29uIGlkPSI5OSIgY2xhc3M9ImZpbDk5IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQxLjQ1LDEuNTcgNDIuMDIsMi4yNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDAiIGNsYXNzPSJmaWwxMDAiIHBvaW50cz0iMjAuMTgsMTkuODMgNDEuOSwyLjEgNDIuNDUsMi43OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDEiIGNsYXNzPSJmaWwxMDEiIHBvaW50cz0iMjAuMTgsMTkuODMgNDIuMzQsMi42NSA0Mi44NywzLjM1ICIvPgogICAgPHBvbHlnb24gaWQ9IjEwMiIgY2xhc3M9ImZpbDEwMiIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Mi43NywzLjIxIDQzLjI4LDMuOTIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTAzIiBjbGFzcz0iZmlsMTAzIiBwb2ludHM9IjIwLjE4LDE5LjgzIDQzLjE4LDMuNzcgNDMuNjgsNC40OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDQiIGNsYXNzPSJmaWwxMDQiIHBvaW50cz0iMjAuMTgsMTkuODMgNDMuNTgsNC4zNSA0NC4wNiw1LjA4ICIvPgogICAgPHBvbHlnb24gaWQ9IjEwNSIgY2xhc3M9ImZpbDEwNSIgcG9pbnRzPSIyMC4xOCwxOS44MyA0My45Niw0Ljk0IDQ0LjQyLDUuNjggIi8+CiAgICA8cG9seWdvbiBpZD0iMTA2IiBjbGFzcz0iZmlsMTA2IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ0LjMzLDUuNTMgNDQuNzcsNi4yOSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDciIGNsYXNzPSJmaWwxMDciIHBvaW50cz0iMjAuMTgsMTkuODMgNDQuNjgsNi4xMyA0NS4xMSw2LjkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTA4IiBjbGFzcz0iZmlsMTA4IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ1LjAyLDYuNzUgNDUuNDMsNy41MiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDkiIGNsYXNzPSJmaWwxMDkiIHBvaW50cz0iMjAuMTgsMTkuODMgNDUuMzUsNy4zNyA0NS43NCw4LjE1ICIvPgogICAgPHBvbHlnb24gaWQ9IjExMCIgY2xhc3M9ImZpbDExMCIgcG9pbnRzPSIyMC4xOCwxOS44MyA0NS42Niw3Ljk5IDQ2LjAzLDguNzkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTExIiBjbGFzcz0iZmlsMTExIiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ1Ljk1LDguNjMgNDYuMyw5LjQzICIvPgogICAgPHBvbHlnb24gaWQ9IjExMiIgY2xhc3M9ImZpbDExMiIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ni4yMyw5LjI3IDQ2LjU2LDEwLjA4ICIvPgogICAgPHBvbHlnb24gaWQ9IjExMyIgY2xhc3M9ImZpbDExMyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ni41LDkuOTIgNDYuODEsMTAuNzMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTE0IiBjbGFzcz0iZmlsMTE0IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ2Ljc0LDEwLjU3IDQ3LjAzLDExLjM5ICIvPgogICAgPHBvbHlnb24gaWQ9IjExNSIgY2xhc3M9ImZpbDExNSIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ni45OCwxMS4yMyA0Ny4yNCwxMi4wNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMTYiIGNsYXNzPSJmaWwxMTYiIHBvaW50cz0iMjAuMTgsMTkuODMgNDcuMTksMTEuODkgNDcuNDQsMTIuNzMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTE3IiBjbGFzcz0iZmlsMTE3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ3LjM5LDEyLjU2IDQ3LjYyLDEzLjQgIi8+CiAgICA8cG9seWdvbiBpZD0iMTE4IiBjbGFzcz0iZmlsMTE4IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ3LjU3LDEzLjIzIDQ3Ljc4LDE0LjA4ICIvPgogICAgPHBvbHlnb24gaWQ9IjExOSIgY2xhc3M9ImZpbDExOSIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ny43NCwxMy45MSA0Ny45MywxNC43NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjAiIGNsYXNzPSJmaWwxMjAiIHBvaW50cz0iMjAuMTgsMTkuODMgNDcuODksMTQuNTkgNDguMDUsMTUuNDUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTIxIiBjbGFzcz0iZmlsMTIxIiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjAyLDE1LjI4IDQ4LjE3LDE2LjEzICIvPgogICAgPHBvbHlnb24gaWQ9IjEyMiIgY2xhc3M9ImZpbDEyMiIgcG9pbnRzPSIyMC4xOCwxOS44MyA0OC4xNCwxNS45NiA0OC4yNiwxNi44MiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjMiIGNsYXNzPSJmaWwxMjMiIHBvaW50cz0iMjAuMTgsMTkuODMgNDguMjQsMTYuNjUgNDguMzQsMTcuNTIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTI0IiBjbGFzcz0iZmlsMTI0IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjMyLDE3LjM0IDQ4LjQsMTguMjEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTI1IiBjbGFzcz0iZmlsMTI1IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjM4LDE4LjA0IDQ4LjQ1LDE4LjkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTI2IiBjbGFzcz0iZmlsMTI2IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjQzLDE4LjczIDQ4LjQ3LDE5LjYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTI3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjQ2LDE5LjQyIDQ4LjQ4LDIwLjI5ICIvPgogICAgPHBvbHlnb24gaWQ9IjEyOCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0OC40OCwyMC4xMiA0OC40OCwyMC45OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDguNDgsMjAuODEgNDguNDUsMjEuNjggIi8+CiAgICA8cG9seWdvbiBpZD0iMTMwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjQ2LDIxLjUgNDguNDEsMjIuMzcgIi8+CiAgICA8cG9seWdvbiBpZD0iMTMxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjQyLDIyLjIgNDguMzUsMjMuMDYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTMyIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjM3LDIyLjg5IDQ4LjI4LDIzLjc1ICIvPgogICAgPHBvbHlnb24gaWQ9IjEzMyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0OC4zLDIzLjU4IDQ4LjE5LDI0LjQ0ICIvPgogICAgPHBvbHlnb24gaWQ9IjEzNCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0OC4yMSwyNC4yNiA0OC4wOCwyNS4xMiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMzUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDguMSwyNC45NSA0Ny45NSwyNS44ICIvPgogICAgPHBvbHlnb24gaWQ9IjEzNiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ny45OCwyNS42MyA0Ny44MSwyNi40OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMzciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDcuODQsMjYuMzEgNDcuNjUsMjcuMTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTM4IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ3LjY5LDI2Ljk4IDQ3LjQ4LDI3LjgyICIvPgogICAgPHBvbHlnb24gaWQ9IjEzOSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ny41MiwyNy42NSA0Ny4yOCwyOC40OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDAiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDcuMzMsMjguMzIgNDcuMDcsMjkuMTQgIi8+CiAgICA8cG9seWdvbiBpZD0iMTQxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ3LjEzLDI4Ljk4IDQ2Ljg1LDI5Ljc5ICIvPgogICAgPHBvbHlnb24gaWQ9IjE0MiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ni45MSwyOS42MyA0Ni42MSwzMC40NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDYuNjcsMzAuMjggNDYuMzUsMzEuMDggIi8+CiAgICA8cG9seWdvbiBpZD0iMTQ0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ2LjQyLDMwLjkyIDQ2LjA4LDMxLjcyICIvPgogICAgPHBvbHlnb24gaWQ9IjE0NSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ni4xNSwzMS41NiA0NS43OSwzMi4zNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDUuODYsMzIuMTggNDUuNDksMzIuOTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTQ3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ1LjU3LDMyLjgxIDQ1LjE3LDMzLjU3ICIvPgogICAgPHBvbHlnb24gaWQ9IjE0OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0NS4yNSwzMy40MiA0NC44NCwzNC4xNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDQuOTIsMzQuMDIgNDQuNDksMzQuNzcgIi8+CiAgICA8cG9seWdvbiBpZD0iMTUwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ0LjU4LDM0LjYyIDQ0LjEzLDM1LjM1ICIvPgogICAgPHBvbHlnb24gaWQ9IjE1MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0NC4yMiwzNS4yMSA0My43NSwzNS45MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNTIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDMuODQsMzUuNzggNDMuMzYsMzYuNSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNTMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDMuNDYsMzYuMzUgNDIuOTUsMzcuMDUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTU0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQzLjA1LDM2LjkxIDQyLjUzLDM3LjYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTU1IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQyLjY0LDM3LjQ2IDQyLjEsMzguMTMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTU2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQyLjIxLDM4IDQxLjY1LDM4LjY2ICIvPgogICAgPHBvbHlnb24gaWQ9IjE1NyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0MS43NywzOC41MiA0MS4yLDM5LjE3ICIvPgogICAgPHBvbHlnb24gaWQ9IjE1OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0MS4zMSwzOS4wNCA0MC43MiwzOS42NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNTkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDAuODQsMzkuNTQgNDAuMjQsNDAuMTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTYwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQwLjM2LDQwLjA0IDM5Ljc0LDQwLjY0ICIvPgogICAgPHBvbHlnb24gaWQ9IjE2MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzOS44Nyw0MC41MiAzOS4yNCw0MS4xICIvPgogICAgPHBvbHlnb24gaWQ9IjE2MiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzOS4zNiw0MC45OCAzOC43Miw0MS41NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNjMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMzguODUsNDEuNDQgMzguMTksNDEuOTkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTY0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDM4LjMyLDQxLjg4IDM3LjY1LDQyLjQxICIvPgogICAgPHBvbHlnb24gaWQ9IjE2NSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzNy43OCw0Mi4zMSAzNy4wOSw0Mi44MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNjYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMzcuMjMsNDIuNzIgMzYuNTMsNDMuMjIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTY3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDM2LjY3LDQzLjEyIDM1Ljk2LDQzLjYxICIvPgogICAgPHBvbHlnb24gaWQ9IjE2OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzNi4xLDQzLjUxIDM1LjM4LDQzLjk4ICIvPgogICAgPHBvbHlnb24gaWQ9IjE2OSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzNS41Miw0My44OCAzNC43OSw0NC4zMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNzAiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMzQuOTMsNDQuMjQgMzQuMTksNDQuNjcgIi8+CiAgICA8cG9seWdvbiBpZD0iMTcxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDM0LjM0LDQ0LjU4IDMzLjU4LDQ0Ljk5ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3MiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzMy43Myw0NC45MSAzMi45Niw0NS4zICIvPgogICAgPHBvbHlnb24gaWQ9IjE3MyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzMy4xMiw0NS4yMyAzMi4zNCw0NS42ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3NCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzMi41LDQ1LjUyIDMxLjcxLDQ1Ljg4ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3NSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzMS44Nyw0NS44MSAzMS4wNyw0Ni4xNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNzYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMzEuMjMsNDYuMDcgMzAuNDMsNDYuMzkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTc3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDMwLjU5LDQ2LjMyIDI5Ljc4LDQ2LjYyICIvPgogICAgPHBvbHlnb24gaWQ9IjE3OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyOS45NCw0Ni41NiAyOS4xMiw0Ni44MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNzkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMjkuMjksNDYuNzggMjguNDYsNDcuMDMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTgwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDI4LjYyLDQ2Ljk4IDI3Ljc5LDQ3LjIyICIvPgogICAgPHBvbHlnb24gaWQ9IjE4MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyNy45Niw0Ny4xNyAyNy4xMiw0Ny4zOCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMjcuMjksNDcuMzQgMjYuNDUsNDcuNTMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTgzIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDI2LjYxLDQ3LjQ5IDI1Ljc3LDQ3LjY2ICIvPgogICAgPHBvbHlnb24gaWQ9IjE4NCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyNS45NCw0Ny42MyAyNS4wOCw0Ny43OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMjUuMjUsNDcuNzUgMjQuNCw0Ny44OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMjQuNTcsNDcuODUgMjMuNzEsNDcuOTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTg3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDIzLjg4LDQ3Ljk0IDIzLjAyLDQ4LjAzICIvPgogICAgPHBvbHlnb24gaWQ9IjE4OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyMy4xOSw0OC4wMSAyMi4zMyw0OC4wNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMjIuNSw0OC4wNiAyMS42NCw0OC4xICIvPgogICAgPHBvbHlnb24gaWQ9IjE5MCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyMS44MSw0OC4xIDIwLjk0LDQ4LjEyICIvPgogICAgPHBvbHlnb24gaWQ9IjE5MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyMS4xMSw0OC4xMSAyMC4yNSw0OC4xMiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOTIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMjAuNDIsNDguMTIgMTkuNTUsNDguMSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOTMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMTkuNzMsNDguMSAxOC44Niw0OC4wNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOTQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMTkuMDMsNDguMDcgMTguMTYsNDggIi8+CiAgICA8cG9seWdvbiBpZD0iMTk1IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDE4LjM0LDQ4LjAyIDE3LjQ3LDQ3LjkzICIvPgogICAgPHBvbHlnb24gaWQ9IjE5NiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAxNy42NSw0Ny45NSAxNi43OCw0Ny44NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOTciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMTYuOTUsNDcuODcgMTYuMDksNDcuNzQgIi8+CiAgICA8cG9seWdvbiBpZD0iMTk4IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDE2LjI3LDQ3Ljc3IDE1LjQxLDQ3LjYyICIvPgogICAgPHBvbHlnb24gaWQ9IjE5OSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAxNS41OCw0Ny42NSAxNC43Miw0Ny40OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDAiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMTQuOSw0Ny41MSAxNC4wNCw0Ny4zMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDEiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMTQuMjEsNDcuMzYgMTMuMzcsNDcuMTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjAyIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDEzLjU0LDQ3LjIgMTIuNyw0Ni45NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMTIuODYsNDcuMDEgMTIuMDMsNDYuNzYgIi8+CiAgICA8cG9seWdvbiBpZD0iMjA0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDEyLjIsNDYuODEgMTEuMzcsNDYuNTQgIi8+CiAgICA8cG9seWdvbiBpZD0iMjA1IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDExLjUzLDQ2LjYgMTAuNzEsNDYuMzEgIi8+CiAgICA8cG9seWdvbiBpZD0iMjA2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDEwLjg3LDQ2LjM2IDEwLjA2LDQ2LjA1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIwNyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAxMC4yMiw0Ni4xMSA5LjQxLDQ1Ljc4ICIvPgogICAgPHBvbHlnb24gaWQ9IjIwOCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA5LjU3LDQ1Ljg1IDguNzcsNDUuNSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgOC45Myw0NS41NyA4LjE0LDQ1LjIgIi8+CiAgICA8cG9seWdvbiBpZD0iMjEwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDguMyw0NS4yNyA3LjUxLDQ0Ljg5ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxMSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA3LjY3LDQ0Ljk2IDYuOSw0NC41NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMTIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNy4wNSw0NC42NCA2LjI5LDQ0LjIxICIvPgogICAgPHBvbHlnb24gaWQ9IjIxMyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA2LjQ0LDQ0LjMgNS42OSw0My44NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMTQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNS44NCw0My45NCA1LjA5LDQzLjQ4ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxNSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA1LjI0LDQzLjU3IDQuNTEsNDMuMDkgIi8+CiAgICA8cG9seWdvbiBpZD0iMjE2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQuNjYsNDMuMTkgMy45NCw0Mi42OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMTciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNC4wOCw0Mi43OSAzLjM3LDQyLjI3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxOCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzLjUyLDQyLjM3IDIuODIsNDEuODQgIi8+CiAgICA8cG9seWdvbiBpZD0iMjE5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDIuOTYsNDEuOTUgMi4yOCw0MS40ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyMCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyLjQxLDQxLjUxIDEuNzQsNDAuOTQgIi8+CiAgICA8cG9seWdvbiBpZD0iMjIxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDEuODgsNDEuMDYgMS4yMiw0MC40NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMS4zNSw0MC41OSAwLjcxLDM5Ljk5ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyMyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAwLjg0LDQwLjExIDAuMjEsMzkuNSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMC4zNCwzOS42MiAtMC4yNywzOSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTAuMTUsMzkuMTIgLTAuNzUsMzguNDggIi8+CiAgICA8cG9seWdvbiBpZD0iMjI2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC0wLjYzLDM4LjYxIC0xLjIxLDM3Ljk1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyNyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMS4wOSwzOC4wOCAtMS42NiwzNy40MSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTEuNTQsMzcuNTUgLTIuMDksMzYuODYgIi8+CiAgICA8cG9seWdvbiBpZD0iMjI5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC0xLjk4LDM3IC0yLjUxLDM2LjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjMwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC0yLjQxLDM2LjQ0IC0yLjkyLDM1LjczICIvPgogICAgPHBvbHlnb24gaWQ9IjIzMSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMi44MiwzNS44OCAtMy4zMiwzNS4xNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMzIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTMuMjIsMzUuMyAtMy43LDM0LjU3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzMyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMy42LDM0LjcxIC00LjA2LDMzLjk3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzNCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMy45NywzNC4xMiAtNC40MSwzMy4zNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMzUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTQuMzIsMzMuNTIgLTQuNzUsMzIuNzUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjM2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC00LjY2LDMyLjkgLTUuMDcsMzIuMTMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjM3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC00Ljk5LDMyLjI4IC01LjM4LDMxLjUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjM4IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC01LjMsMzEuNjYgLTUuNjcsMzAuODYgIi8+CiAgICA8cG9seWdvbiBpZD0iMjM5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC01LjU5LDMxLjAyIC01Ljk0LDMwLjIyICIvPgogICAgPHBvbHlnb24gaWQ9IjI0MCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNS44NywzMC4zOCAtNi4yLDI5LjU3ICIvPgogICAgPHBvbHlnb24gaWQ9IjI0MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNi4xNCwyOS43MyAtNi40NCwyOC45MiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTYuMzgsMjkuMDggLTYuNjcsMjguMjYgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQzIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC02LjYxLDI4LjQyIC02Ljg4LDI3LjU5ICIvPgogICAgPHBvbHlnb24gaWQ9IjI0NCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNi44MywyNy43NiAtNy4wOCwyNi45MiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuMDMsMjcuMDkgLTcuMjYsMjYuMjUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQ2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC03LjIxLDI2LjQyIC03LjQyLDI1LjU3ICIvPgogICAgPHBvbHlnb24gaWQ9IjI0NyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNy4zOCwyNS43NCAtNy41NiwyNC44OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuNTMsMjUuMDYgLTcuNjksMjQuMiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuNjYsMjQuMzcgLTcuODEsMjMuNTIgIi8+CiAgICA8cG9seWdvbiBpZD0iMjUwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC03Ljc4LDIzLjY5IC03LjksMjIuODMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjUxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC03Ljg4LDIzIC03Ljk4LDIyLjE0ICIvPgogICAgPHBvbHlnb24gaWQ9IjI1MiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNy45NiwyMi4zMSAtOC4wNCwyMS40NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNTMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTguMDIsMjEuNjIgLTguMDgsMjAuNzUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjU0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC04LjA3LDIwLjkyIC04LjExLDIwLjA1ICIvPgogICAgPHBvbHlnb24gaWQ9IjI1NSIgY2xhc3M9ImZpbDEyOCIgcG9pbnRzPSIyMC4xOCwxOS44MyAtOC4xLDIwLjIzIC04LjEyLDE5LjUzICIvPgogICA8L2c+CiAgPC9nPgogPC9nPgo8L3N2Zz4=");
}
.semicircle-2qn7A4BC{
	position:absolute;
	left:5px;
	top:5px;
	width:210px;
	height:105px;
	border-top-left-radius:210px;
	border-top-right-radius:210px;
	transition:box-shadow 1.5s ease;
	-webkit-mask-image:linear-gradient(0deg,transparent,#000 30px);
	mask-image:linear-gradient(0deg,transparent,#000 30px)
}
.semicircleNeutral-2qn7A4BC{
	box-shadow:inset 0 30px 60px -10px var(--HBRGBA25);
}
html.theme-dark .semicircleNeutral-2qn7A4BC{
	box-shadow:inset 0 30px 60px -10px var(--HBRGBA25);
}
.semicircleBuy-2qn7A4BC{
	box-shadow:inset 0 30px 60px -10px var(--GRNRGBA25);
}
.semicircleStrongBuy-2qn7A4BC{
	box-shadow:inset 0 30px 60px -10px var(--GRNRGBA50);
}
.semicircleSell-2qn7A4BC{
	box-shadow:inset 0 30px 60px -10px var(--REDRGBA25);
}
.semicircleStrongSell-2qn7A4BC{
	box-shadow:inset 0 30px 60px -10px var(--REDRGBA50);
}
.dot-2qn7A4BC{
	position:absolute;
	box-sizing:border-box;
	width:8px;
	height:8px;
	bottom:0;
	border:2px solid #131722;
	left:calc(50%-4px);
	border-radius:50%
}
html.theme-dark .dot-2qn7A4BC{
	border:2px solid #b2b5be
}
.arrow-2qn7A4BC{
	display:flex;
	position:absolute;
	flex-direction:column;
	justify-content:center;
	align-items:center;
	width:8px;
	height:97px;
	bottom:4px;
	left:calc(50%-4px);
	transform-origin:50% 100%;
	transition:transform 1.5s ease
}
.arrowHidden-2qn7A4BC{
	width:2px;
	height:8px;
	visibility:hidden
}
.arrowMain-2qn7A4BC{
	width:2px;
	height:90px;
	border-radius:1px;
	background-color:#131722
}
html.theme-dark .arrowMain-2qn7A4BC{
	background-color:#b2b5be
}
.arrowNeutral-2qn7A4BC{
	transform:rotate(0deg)
}
.arrowBuy-2qn7A4BC{
	transform:rotate(36deg)
}
.arrowStrongBuy-2qn7A4BC{
	transform:rotate(72deg)
}
.arrowSell-2qn7A4BC{
	transform:rotate(-36deg)
}
.arrowStrongSell-2qn7A4BC{
	transform:rotate(-72deg)
}
.arrowShudderNeutral-2qn7A4BC{
	animation:NeutralShudder-2qn7A4BC 10s infinite
}
.arrowShudderBuy-2qn7A4BC{
	animation:buyShudder-2qn7A4BC 10s infinite
}
.arrowShudderStrongBuy-2qn7A4BC{
	animation:strongBuyShudder-2qn7A4BC 10s infinite
}
.arrowShudderSell-2qn7A4BC{
	animation:sellShudder-2qn7A4BC 10s infinite
}
.arrowShudderStrongSell-2qn7A4BC{
	animation:strongSellShudder-2qn7A4BC 10s infinite
}
@keyframes buyShudder-2qn7A4BC{
	0%{
		transform:rotate(36deg)
}
	35%{
		transform:rotate(34deg)
}
	40%{
		transform:rotate(36deg)
}
	45%{
		transform:rotate(33deg)
}
	60%{
		transform:rotate(31deg)
}
	80%{
		transform:rotate(35deg)
}
	90%{
		transform:rotate(37deg)
}
	to{
		transform:rotate(36deg)
}
}
@keyframes strongBuyShudder-2qn7A4BC{
	0%{
		transform:rotate(72deg)
}
	35%{
		transform:rotate(70deg)
}
	40%{
		transform:rotate(72deg)
}
	45%{
		transform:rotate(69deg)
}
	60%{
		transform:rotate(67deg)
}
	80%{
		transform:rotate(69deg)
}
	90%{
		transform:rotate(73deg)
}
	to{
		transform:rotate(72deg)
}
}
@keyframes sellShudder-2qn7A4BC{
	0%{
		transform:rotate(-36deg)
}
	35%{
		transform:rotate(-34deg)
}
	40%{
		transform:rotate(-36deg)
}
	45%{
		transform:rotate(-33deg)
}
	60%{
		transform:rotate(-31deg)
}
	80%{
		transform:rotate(-35deg)
}
	90%{
		transform:rotate(-37deg)
}
	to{
		transform:rotate(-36deg)
}
}
@keyframes strongSellShudder-2qn7A4BC{
	0%{
		transform:rotate(-72deg)
}
	35%{
		transform:rotate(-70deg)
}
	40%{
		transform:rotate(-72deg)
}
	45%{
		transform:rotate(-69deg)
}
	60%{
		transform:rotate(-67deg)
}
	80%{
		transform:rotate(-69deg)
}
	90%{
		transform:rotate(-73deg)
}
	to{
		transform:rotate(-72deg)
}
}
@keyframes NeutralShudder-2qn7A4BC{
	0%{
		transform:rotate(0deg)
}
	35%{
		transform:rotate(-2deg)
}
	40%{
		transform:rotate(0deg)
}
	45%{
		transform:rotate(-3deg)
}
	60%{
		transform:rotate(-5deg)
}
	80%{
		transform:rotate(-3deg)
}
	90%{
		transform:rotate(1deg)
}
	to{
		transform:rotate(0deg)
}
}
@media screen and (min-width:499.5px){
	.large-2qn7A4BC .speedometerTextWrapper-2qn7A4BC{
		width:100%;
		left:0
}
	.large-2qn7A4BC .sizeWrapper-2qn7A4BC{
		width:316px;
		height:158px;
		margin-top:25px
}
	.large-2qn7A4BC .bottomSignals-2qn7A4BC,.large-2qn7A4BC .middleSignals-2qn7A4BC{
		margin:32px 0
}
	.large-2qn7A4BC .middleSignals-2qn7A4BC{
		width:104%
}
	.large-2qn7A4BC .bottomSignals-2qn7A4BC{
		width:140%
}
	.large-2qn7A4BC .speedometerText-2qn7A4BC{
		font-size:12px
}
	.large-2qn7A4BC .circleWrapper-2qn7A4BC{
		width:316px;
		height:158px;
        background-image:url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbDpzcGFjZT0icHJlc2VydmUiIHdpZHRoPSIzMTZweCIgaGVpZ2h0PSIxNThweCIgdmVyc2lvbj0iMS4xIiBzdHlsZT0ic2hhcGUtcmVuZGVyaW5nOmdlb21ldHJpY1ByZWNpc2lvbjsgdGV4dC1yZW5kZXJpbmc6Z2VvbWV0cmljUHJlY2lzaW9uOyBpbWFnZS1yZW5kZXJpbmc6b3B0aW1pemVRdWFsaXR5OyBmaWxsLXJ1bGU6ZXZlbm9kZDsgY2xpcC1ydWxlOmV2ZW5vZGQiCnZpZXdCb3g9IjAgMCA1Ny4wNiAyOC41MyIKIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIj4KIDxkZWZzPgogIDxzdHlsZSB0eXBlPSJ0ZXh0L2NzcyI+CiAgIDwhW0NEQVRBWwogICAgLmZpbDY0IHtmaWxsOiMwMEIyQzZ9CiAgICAuZmlsNjMge2ZpbGw6IzAwQjJDOH0KICAgIC5maWw2NyB7ZmlsbDojMDBCM0MwfQogICAgLmZpbDY2IHtmaWxsOiMwMEIzQzJ9CiAgICAuZmlsNjUge2ZpbGw6IzAwQjNDNH0KICAgIC5maWw3MCB7ZmlsbDojMDBCNEJCfQogICAgLmZpbDY5IHtmaWxsOiMwMEI0QkR9CiAgICAuZmlsNjgge2ZpbGw6IzAwQjRCRn0KICAgIC5maWw3MyB7ZmlsbDojMDBCNUI2fQogICAgLmZpbDcyIHtmaWxsOiMwMEI1Qjh9CiAgICAuZmlsNzEge2ZpbGw6IzAwQjVCOX0KICAgIC5maWw3NiB7ZmlsbDojMDBCNkIxfQogICAgLmZpbDc1IHtmaWxsOiMwMEI2QjJ9CiAgICAuZmlsNzQge2ZpbGw6IzAwQjZCNH0KICAgIC5maWw3OSB7ZmlsbDojMDBCN0FCfQogICAgLmZpbDc4IHtmaWxsOiMwMEI3QUR9CiAgICAuZmlsNzcge2ZpbGw6IzAwQjdBRn0KICAgIC5maWw4MiB7ZmlsbDojMDBCOEE2fQogICAgLmZpbDgxIHtmaWxsOiMwMEI4QTh9CiAgICAuZmlsODAge2ZpbGw6IzAwQjhBOX0KICAgIC5maWw4NSB7ZmlsbDojMDBCOUExfQogICAgLmZpbDg0IHtmaWxsOiMwMEI5QTJ9CiAgICAuZmlsODMge2ZpbGw6IzAwQjlBNH0KICAgIC5maWw4OCB7ZmlsbDojMDBCQTlCfQogICAgLmZpbDg3IHtmaWxsOiMwMEJBOUR9CiAgICAuZmlsODYge2ZpbGw6IzAwQkE5Rn0KICAgIC5maWw5MSB7ZmlsbDojMDBCQjk2fQogICAgLmZpbDkwIHtmaWxsOiMwMEJCOTh9CiAgICAuZmlsODkge2ZpbGw6IzAwQkI5OX0KICAgIC5maWw5NCB7ZmlsbDojMDBCQzkxfQogICAgLmZpbDkzIHtmaWxsOiMwMEJDOTJ9CiAgICAuZmlsOTIge2ZpbGw6IzAwQkM5NH0KICAgIC5maWw5NyB7ZmlsbDojMDBCRDhCfQogICAgLmZpbDk2IHtmaWxsOiMwMEJEOER9CiAgICAuZmlsOTUge2ZpbGw6IzAwQkQ4Rn0KICAgIC5maWwxMDAge2ZpbGw6IzAwQkU4Nn0KICAgIC5maWw5OSB7ZmlsbDojMDBCRTg4fQogICAgLmZpbDk4IHtmaWxsOiMwMEJFOEF9CiAgICAuZmlsMTAzIHtmaWxsOiMwMEJGODF9CiAgICAuZmlsMTAyIHtmaWxsOiMwMEJGODJ9CiAgICAuZmlsMTAxIHtmaWxsOiMwMEJGODR9CiAgICAuZmlsMTA2IHtmaWxsOiMwMEMwN0J9CiAgICAuZmlsMTA1IHtmaWxsOiMwMEMwN0R9CiAgICAuZmlsMTA0IHtmaWxsOiMwMEMwN0Z9CiAgICAuZmlsMTA5IHtmaWxsOiMwMEMxNzZ9CiAgICAuZmlsMTA4IHtmaWxsOiMwMEMxNzh9CiAgICAuZmlsMTA3IHtmaWxsOiMwMEMxN0F9CiAgICAuZmlsMTEyIHtmaWxsOiMwMEMyNzF9CiAgICAuZmlsMTExIHtmaWxsOiMwMEMyNzJ9CiAgICAuZmlsMTEwIHtmaWxsOiMwMEMyNzR9CiAgICAuZmlsMTE1IHtmaWxsOiMwMEMzNkJ9CiAgICAuZmlsMTE0IHtmaWxsOiMwMEMzNkR9CiAgICAuZmlsMTEzIHtmaWxsOiMwMEMzNkZ9CiAgICAuZmlsMTE4IHtmaWxsOiMwMEM0NjZ9CiAgICAuZmlsMTE3IHtmaWxsOiMwMEM0Njh9CiAgICAuZmlsMTE2IHtmaWxsOiMwMEM0NkF9CiAgICAuZmlsMTIxIHtmaWxsOiMwMEM1NjF9CiAgICAuZmlsMTIwIHtmaWxsOiMwMEM1NjN9CiAgICAuZmlsMTE5IHtmaWxsOiMwMEM1NjR9CiAgICAuZmlsMTI0IHtmaWxsOiMwMEM2NUJ9CiAgICAuZmlsMTIzIHtmaWxsOiMwMEM2NUR9CiAgICAuZmlsMTIyIHtmaWxsOiMwMEM2NUZ9CiAgICAuZmlsMTI3IHtmaWxsOiMwMEM3NTd9CiAgICAuZmlsMTI2IHtmaWxsOiMwMEM3NTh9CiAgICAuZmlsMTI1IHtmaWxsOiMwMEM3NUF9CiAgICAuZmlsNjIge2ZpbGw6IzAzQjBDNn0KICAgIC5maWw2MSB7ZmlsbDojMDdBREM0fQogICAgLmZpbDYwIHtmaWxsOiMwQkFBQzJ9CiAgICAuZmlsNTkge2ZpbGw6IzBGQThDMH0KICAgIC5maWw1OCB7ZmlsbDojMTNBNUJFfQogICAgLmZpbDU3IHtmaWxsOiMxN0EyQkN9CiAgICAuZmlsNTYge2ZpbGw6IzFCOUZCQX0KICAgIC5maWw1NSB7ZmlsbDojMUY5Q0I3fQogICAgLmZpbDU0IHtmaWxsOiMyMzlBQjV9CiAgICAuZmlsNTMge2ZpbGw6IzI3OTdCM30KICAgIC5maWw1MiB7ZmlsbDojMkI5NEIxfQogICAgLmZpbDUxIHtmaWxsOiMyRjkxQUZ9CiAgICAuZmlsNTAge2ZpbGw6IzMzOEVBRH0KICAgIC5maWw0OSB7ZmlsbDojMzc4Q0FCfQogICAgLmZpbDQ4IHtmaWxsOiMzQjg5QTl9CiAgICAuZmlsNDcge2ZpbGw6IzNGODZBNn0KICAgIC5maWw0NiB7ZmlsbDojNDM4M0E0fQogICAgLmZpbDQ1IHtmaWxsOiM0NzgwQTJ9CiAgICAuZmlsNDQge2ZpbGw6IzRCN0VBMH0KICAgIC5maWw0MyB7ZmlsbDojNEY3QjlFfQogICAgLmZpbDQyIHtmaWxsOiM1Mzc4OUN9CiAgICAuZmlsNDEge2ZpbGw6IzU3NzU5QX0KICAgIC5maWw0MCB7ZmlsbDojNUI3Mjk3fQogICAgLmZpbDM5IHtmaWxsOiM1RjcwOTV9CiAgICAuZmlsMzgge2ZpbGw6IzYzNkQ5M30KICAgIC5maWwzNyB7ZmlsbDojNjc2QTkxfQogICAgLmZpbDM2IHtmaWxsOiM2QjY3OEZ9CiAgICAuZmlsMzUge2ZpbGw6IzZGNjU4RH0KICAgIC5maWwzNCB7ZmlsbDojNzM2MjhCfQogICAgLmZpbDMzIHtmaWxsOiM3NzVGODl9CiAgICAuZmlsMzIge2ZpbGw6IzdCNUM4Nn0KICAgIC5maWwzMSB7ZmlsbDojN0Y1OTg0fQogICAgLmZpbDMwIHtmaWxsOiM4MzU3ODJ9CiAgICAuZmlsMjkge2ZpbGw6Izg3NTQ4MH0KICAgIC5maWwyOCB7ZmlsbDojOEI1MTdFfQogICAgLmZpbDI3IHtmaWxsOiM4RjRFN0N9CiAgICAuZmlsMjYge2ZpbGw6IzkzNEI3QX0KICAgIC5maWwyNSB7ZmlsbDojOTc0OTc3fQogICAgLmZpbDI0IHtmaWxsOiM5QjQ2NzV9CiAgICAuZmlsMjMge2ZpbGw6IzlGNDM3M30KICAgIC5maWwyMiB7ZmlsbDojQTM0MDcxfQogICAgLmZpbDIxIHtmaWxsOiNBNzNENkZ9CiAgICAuZmlsMjAge2ZpbGw6I0FCM0I2RH0KICAgIC5maWwxOSB7ZmlsbDojQUYzODZCfQogICAgLmZpbDE4IHtmaWxsOiNCMzM1Njl9CiAgICAuZmlsMTcge2ZpbGw6I0I3MzI2Nn0KICAgIC5maWwxNiB7ZmlsbDojQkIyRjY0fQogICAgLmZpbDE1IHtmaWxsOiNCRjJENjJ9CiAgICAuZmlsMTQge2ZpbGw6I0MzMkE2MH0KICAgIC5maWwxMyB7ZmlsbDojQzcyNzVFfQogICAgLmZpbDEyIHtmaWxsOiNDQjI0NUN9CiAgICAuZmlsMTEge2ZpbGw6I0NGMjI1QX0KICAgIC5maWwxMCB7ZmlsbDojRDMxRjU3fQogICAgLmZpbDkge2ZpbGw6I0Q3MUM1NX0KICAgIC5maWw4IHtmaWxsOiNEQjE5NTN9CiAgICAuZmlsNyB7ZmlsbDojREYxNjUxfQogICAgLmZpbDYge2ZpbGw6I0UzMTQ0Rn0KICAgIC5maWw1IHtmaWxsOiNFNzExNER9CiAgICAuZmlsNCB7ZmlsbDojRUIwRTRCfQogICAgLmZpbDMge2ZpbGw6I0VGMEI0OX0KICAgIC5maWwyIHtmaWxsOiNGMzA4NDZ9CiAgICAuZmlsMSB7ZmlsbDojRjcwNjQ0fQogICAgLmZpbDAge2ZpbGw6I0ZCMDM0Mn0KICAgIC5maWwxMjgge2ZpbGw6I0ZGMDA0MH0KICAgXV0+CiAgPC9zdHlsZT4KICAgIDxjbGlwUGF0aCBpZD0iaWQwIj4KICAgICA8cGF0aCBkPSJNNS4wMyAxMi4zNWMwLjA2LC0wLjA5IDAuMTcsLTAuMTUgMC4yOSwtMC4xNSAwLjA4LDAgMC4xNSwwLjAyIDAuMjEsMC4wNyAwLjE2LDAuMTEgMC4yLDAuMzQgMC4wOSwwLjUgLTMuMTMsNC41MyAtNC44NCw5LjkgLTQuOSwxNS40IDAsMC4yIC0wLjE2LDAuMzYgLTAuMzYsMC4zNiAtMC4yLDAgLTAuMzYsLTAuMTYgLTAuMzYsLTAuMzYgMCwwIDAsMCAwLDAgMC4wNywtNS44NyAxLjkyLC0xMS4zMSA1LjAzLC0xNS44MmwwIDB6bTQ2LjUgLTAuMDhjLTAuMDksMC4wNyAtMC4xNSwwLjE4IC0wLjE1LDAuMjkgMCwwLjA4IDAuMDIsMC4xNSAwLjA2LDAuMjEgMy4xMyw0LjUzIDQuODQsOS45IDQuOSwxNS40IDAsMC4yIDAuMTYsMC4zNiAwLjM2LDAuMzYgMC4yLDAgMC4zNiwtMC4xNiAwLjM2LC0wLjM2IDAsMCAwLDAgMCwwIC0wLjA1LC01LjY1IC0xLjgxLC0xMS4xNiAtNS4wMiwtMTUuODIgLTAuMDcsLTAuMDkgLTAuMTgsLTAuMTUgLTAuMywtMC4xNSAtMC4wNywwIC0wLjE1LDAuMDIgLTAuMjEsMC4wN2wwIDB6bS0xMy42MyAtOS45M2MtMC4xNSwtMC4wNSAtMC4yNCwtMC4xOSAtMC4yNCwtMC4zNCAwLC0wLjA0IDAsLTAuMDggMC4wMiwtMC4xMiAwLjA0LC0wLjE0IDAuMTgsLTAuMjQgMC4zNCwtMC4yNCAwLjA0LDAgMC4wOCwwIDAuMTEsMC4wMiA1LjE3LDEuODUgOS43MSw1LjE2IDEzLjA1LDkuNTIgMC4xMiwwLjE2IDAuMDksMC4zOSAtMC4wOCwwLjUgLTAuMDYsMC4wNSAtMC4xMywwLjA3IC0wLjIxLDAuMDcgLTAuMTEsMCAtMC4yMiwtMC4wNSAtMC4yOSwtMC4xNCAtMy4yNSwtNC4yNCAtNy42NywtNy40NiAtMTIuNywtOS4yN2wwIDB6bS0xNy44MyAtMC42OGMwLjA1LDAuMTUgMC4xOSwwLjI1IDAuMzUsMC4yNSAwLjAzLDAgMC4wNywtMC4wMSAwLjEsLTAuMDIgMi41OSwtMC43NyA1LjI4LC0xLjE3IDcuOTksLTEuMTcgMCwwIDAuMDEsMCAwLjAyLDAgMi43OCwwIDUuNDcsMC40MSA4LjAxLDEuMTcgMC4wMywwLjAxIDAuMDcsMC4wMiAwLjEsMC4wMiAwLjE2LDAgMC4zLC0wLjEgMC4zNSwtMC4yNSAwLjAxLC0wLjA0IDAuMDIsLTAuMDggMC4wMiwtMC4xMiAwLC0wLjE1IC0wLjExLC0wLjI5IC0wLjI2LC0wLjM0IC0yLjY1LC0wLjc5IC01LjQyLC0xLjIgLTguMTksLTEuMiAtMC4wMSwwIC0wLjAyLDAgLTAuMDMsMCAtMi44NiwwIC01LjYyLDAuNDIgLTguMjIsMS4yIC0wLjE1LDAuMDUgLTAuMjUsMC4xOSAtMC4yNSwwLjM0IDAsMC4wNCAwLDAuMDggMC4wMSwwLjEybDAgMHptLTAuNjggMC4yMmMwLjAxLDAuMDQgMC4wMiwwLjA4IDAuMDIsMC4xMiAwLDAuMTUgLTAuMSwwLjI5IC0wLjI1LDAuMzQgLTUuMDMsMS44IC05LjQ1LDUuMDMgLTEyLjcsOS4yNyAtMC4wNywwLjA5IC0wLjE4LDAuMTQgLTAuMjksMC4xNCAtMC4wOCwwIC0wLjE1LC0wLjAyIC0wLjIxLC0wLjA3IC0wLjEsLTAuMDYgLTAuMTUsLTAuMTcgLTAuMTUsLTAuMjkgMCwtMC4wNyAwLjAzLC0wLjE1IDAuMDcsLTAuMjEgMy4zNCwtNC4zNiA3Ljg4LC03LjY3IDEzLjA1LC05LjUyIDAuMTksLTAuMDcgMC4zOSwwLjAzIDAuNDYsMC4yMmwwIDB6Ii8+CiAgICA8L2NsaXBQYXRoPgogPC9kZWZzPgogPGcgaWQ9IjEiPgogIDxnPgogICA8ZyBzdHlsZT0iY2xpcC1wYXRoOnVybCgjaWQwKSI+CiAgICA8cG9seWdvbiBjbGFzcz0iZmlsMCIgcG9pbnRzPSIyOC45OSwyOC40OCAtMTEuNjYsMjguMzEgLTExLjY2LDI2LjgxICIvPgogICAgPHBvbHlnb24gaWQ9IjEiIGNsYXNzPSJmaWwxIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMS42NiwyNy4wNiAtMTEuNjIsMjUuODEgIi8+CiAgICA8cG9seWdvbiBpZD0iMiIgY2xhc3M9ImZpbDIiIHBvaW50cz0iMjguOTksMjguNDggLTExLjYzLDI2LjA2IC0xMS41NiwyNC44MiAiLz4KICAgIDxwb2x5Z29uIGlkPSIzIiBjbGFzcz0iZmlsMyIgcG9pbnRzPSIyOC45OSwyOC40OCAtMTEuNTgsMjUuMDcgLTExLjQ4LDIzLjgzICIvPgogICAgPHBvbHlnb24gaWQ9IjQiIGNsYXNzPSJmaWw0IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMS41LDI0LjA4IC0xMS4zNywyMi44NCAiLz4KICAgIDxwb2x5Z29uIGlkPSI1IiBjbGFzcz0iZmlsNSIgcG9pbnRzPSIyOC45OSwyOC40OCAtMTEuNCwyMy4wOSAtMTEuMjQsMjEuODUgIi8+CiAgICA8cG9seWdvbiBpZD0iNiIgY2xhc3M9ImZpbDYiIHBvaW50cz0iMjguOTksMjguNDggLTExLjI3LDIyLjEgLTExLjA4LDIwLjg3ICIvPgogICAgPHBvbHlnb24gaWQ9IjciIGNsYXNzPSJmaWw3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMS4xMiwyMS4xMiAtMTAuOSwxOS44OSAiLz4KICAgIDxwb2x5Z29uIGlkPSI4IiBjbGFzcz0iZmlsOCIgcG9pbnRzPSIyOC45OSwyOC40OCAtMTAuOTUsMjAuMTQgLTEwLjcsMTguOTIgIi8+CiAgICA8cG9seWdvbiBpZD0iOSIgY2xhc3M9ImZpbDkiIHBvaW50cz0iMjguOTksMjguNDggLTEwLjc1LDE5LjE2IC0xMC40NywxNy45NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMCIgY2xhc3M9ImZpbDEwIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMC41MywxOC4yIC0xMC4yMiwxNi45OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMSIgY2xhc3M9ImZpbDExIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMC4yOCwxNy4yMyAtOS45NCwxNi4wNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMiIgY2xhc3M9ImZpbDEyIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMC4wMSwxNi4yOCAtOS42NCwxNS4xICIvPgogICAgPHBvbHlnb24gaWQ9IjEzIiBjbGFzcz0iZmlsMTMiIHBvaW50cz0iMjguOTksMjguNDggLTkuNzIsMTUuMzMgLTkuMzIsMTQuMTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTQiIGNsYXNzPSJmaWwxNCIgcG9pbnRzPSIyOC45OSwyOC40OCAtOS40LDE0LjM5IC04Ljk4LDEzLjIzICIvPgogICAgPHBvbHlnb24gaWQ9IjE1IiBjbGFzcz0iZmlsMTUiIHBvaW50cz0iMjguOTksMjguNDggLTkuMDYsMTMuNDYgLTguNjEsMTIuMzEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTYiIGNsYXNzPSJmaWwxNiIgcG9pbnRzPSIyOC45OSwyOC40OCAtOC43LDEyLjU0IC04LjIyLDExLjQgIi8+CiAgICA8cG9seWdvbiBpZD0iMTciIGNsYXNzPSJmaWwxNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtOC4zMSwxMS42MyAtNy44LDEwLjUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTgiIGNsYXNzPSJmaWwxOCIgcG9pbnRzPSIyOC45OSwyOC40OCAtNy45MSwxMC43MiAtNy4zNyw5LjYxICIvPgogICAgPHBvbHlnb24gaWQ9IjE5IiBjbGFzcz0iZmlsMTkiIHBvaW50cz0iMjguOTksMjguNDggLTcuNDgsOS44MyAtNi45MSw4LjczICIvPgogICAgPHBvbHlnb24gaWQ9IjIwIiBjbGFzcz0iZmlsMjAiIHBvaW50cz0iMjguOTksMjguNDggLTcuMDIsOC45NSAtNi40Myw3Ljg3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxIiBjbGFzcz0iZmlsMjEiIHBvaW50cz0iMjguOTksMjguNDggLTYuNTUsOC4wOCAtNS45Myw3LjAxICIvPgogICAgPHBvbHlnb24gaWQ9IjIyIiBjbGFzcz0iZmlsMjIiIHBvaW50cz0iMjguOTksMjguNDggLTYuMDUsNy4yMyAtNS40MSw2LjE3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzIiBjbGFzcz0iZmlsMjMiIHBvaW50cz0iMjguOTksMjguNDggLTUuNTQsNi4zOCAtNC44Nyw1LjM0ICIvPgogICAgPHBvbHlnb24gaWQ9IjI0IiBjbGFzcz0iZmlsMjQiIHBvaW50cz0iMjguOTksMjguNDggLTUsNS41NSAtNC4zLDQuNTMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjUiIGNsYXNzPSJmaWwyNSIgcG9pbnRzPSIyOC45OSwyOC40OCAtNC40NCw0Ljc0IC0zLjcyLDMuNzMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjYiIGNsYXNzPSJmaWwyNiIgcG9pbnRzPSIyOC45OSwyOC40OCAtMy44NywzLjkzIC0zLjEyLDIuOTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjciIGNsYXNzPSJmaWwyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtMy4yNywzLjE1IC0yLjUsMi4xOCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyOCIgY2xhc3M9ImZpbDI4IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0yLjY1LDIuMzcgLTEuODYsMS40MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyOSIgY2xhc3M9ImZpbDI5IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0yLjAyLDEuNjIgLTEuMiwwLjY5ICIvPgogICAgPHBvbHlnb24gaWQ9IjMwIiBjbGFzcz0iZmlsMzAiIHBvaW50cz0iMjguOTksMjguNDggLTEuMzYsMC44OCAtMC41MiwtMC4wMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIzMSIgY2xhc3M9ImZpbDMxIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0wLjY5LDAuMTUgMC4xNywtMC43MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIzMiIgY2xhc3M9ImZpbDMyIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDAsLTAuNTUgMC44OSwtMS40MSAiLz4KICAgIDxwb2x5Z29uIGlkPSIzMyIgY2xhc3M9ImZpbDMzIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDAuNzEsLTEuMjQgMS42MiwtMi4wOCAiLz4KICAgIDxwb2x5Z29uIGlkPSIzNCIgY2xhc3M9ImZpbDM0IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDEuNDMsLTEuOTEgMi4zNiwtMi43MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIzNSIgY2xhc3M9ImZpbDM1IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDIuMTgsLTIuNTcgMy4xMiwtMy4zNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIzNiIgY2xhc3M9ImZpbDM2IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDIuOTMsLTMuMiAzLjksLTMuOTcgIi8+CiAgICA8cG9seWdvbiBpZD0iMzciIGNsYXNzPSJmaWwzNyIgcG9pbnRzPSIyOC45OSwyOC40OCAzLjcxLC0zLjgyIDQuNjksLTQuNTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMzgiIGNsYXNzPSJmaWwzOCIgcG9pbnRzPSIyOC45OSwyOC40OCA0LjUsLTQuNDEgNS41LC01LjEzICIvPgogICAgPHBvbHlnb24gaWQ9IjM5IiBjbGFzcz0iZmlsMzkiIHBvaW50cz0iMjguOTksMjguNDggNS4zLC00Ljk5IDYuMzIsLTUuNjggIi8+CiAgICA8cG9seWdvbiBpZD0iNDAiIGNsYXNzPSJmaWw0MCIgcG9pbnRzPSIyOC45OSwyOC40OCA2LjEyLC01LjU0IDcuMTYsLTYuMjEgIi8+CiAgICA8cG9seWdvbiBpZD0iNDEiIGNsYXNzPSJmaWw0MSIgcG9pbnRzPSIyOC45OSwyOC40OCA2Ljk1LC02LjA4IDguMDEsLTYuNzIgIi8+CiAgICA8cG9seWdvbiBpZD0iNDIiIGNsYXNzPSJmaWw0MiIgcG9pbnRzPSIyOC45OSwyOC40OCA3Ljc5LC02LjU5IDguODcsLTcuMjEgIi8+CiAgICA8cG9seWdvbiBpZD0iNDMiIGNsYXNzPSJmaWw0MyIgcG9pbnRzPSIyOC45OSwyOC40OCA4LjY1LC03LjA5IDkuNzQsLTcuNjggIi8+CiAgICA8cG9seWdvbiBpZD0iNDQiIGNsYXNzPSJmaWw0NCIgcG9pbnRzPSIyOC45OSwyOC40OCA5LjUyLC03LjU2IDEwLjYyLC04LjEyICIvPgogICAgPHBvbHlnb24gaWQ9IjQ1IiBjbGFzcz0iZmlsNDUiIHBvaW50cz0iMjguOTksMjguNDggMTAuNCwtOC4wMSAxMS41MiwtOC41NCAiLz4KICAgIDxwb2x5Z29uIGlkPSI0NiIgY2xhc3M9ImZpbDQ2IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDExLjMsLTguNDQgMTIuNDMsLTguOTQgIi8+CiAgICA8cG9seWdvbiBpZD0iNDciIGNsYXNzPSJmaWw0NyIgcG9pbnRzPSIyOC45OSwyOC40OCAxMi4yLC04Ljg0IDEzLjM0LC05LjMyICIvPgogICAgPHBvbHlnb24gaWQ9IjQ4IiBjbGFzcz0iZmlsNDgiIHBvaW50cz0iMjguOTksMjguNDggMTMuMTEsLTkuMjMgMTQuMjcsLTkuNjggIi8+CiAgICA8cG9seWdvbiBpZD0iNDkiIGNsYXNzPSJmaWw0OSIgcG9pbnRzPSIyOC45OSwyOC40OCAxNC4wNCwtOS41OSAxNS4yLC0xMC4wMSAiLz4KICAgIDxwb2x5Z29uIGlkPSI1MCIgY2xhc3M9ImZpbDUwIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDE0Ljk3LC05LjkyIDE2LjE0LC0xMC4zMiAiLz4KICAgIDxwb2x5Z29uIGlkPSI1MSIgY2xhc3M9ImZpbDUxIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDE1LjkxLC0xMC4yNCAxNy4wOSwtMTAuNiAiLz4KICAgIDxwb2x5Z29uIGlkPSI1MiIgY2xhc3M9ImZpbDUyIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDE2Ljg2LC0xMC41MyAxOC4wNSwtMTAuODcgIi8+CiAgICA8cG9seWdvbiBpZD0iNTMiIGNsYXNzPSJmaWw1MyIgcG9pbnRzPSIyOC45OSwyOC40OCAxNy44MSwtMTAuOCAxOS4wMiwtMTEuMSAiLz4KICAgIDxwb2x5Z29uIGlkPSI1NCIgY2xhc3M9ImZpbDU0IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDE4Ljc4LC0xMS4wNCAxOS45OSwtMTEuMzIgIi8+CiAgICA8cG9seWdvbiBpZD0iNTUiIGNsYXNzPSJmaWw1NSIgcG9pbnRzPSIyOC45OSwyOC40OCAxOS43NCwtMTEuMjYgMjAuOTYsLTExLjUxICIvPgogICAgPHBvbHlnb24gaWQ9IjU2IiBjbGFzcz0iZmlsNTYiIHBvaW50cz0iMjguOTksMjguNDggMjAuNzIsLTExLjQ2IDIxLjk0LC0xMS42OCAiLz4KICAgIDxwb2x5Z29uIGlkPSI1NyIgY2xhc3M9ImZpbDU3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDIxLjcsLTExLjYzIDIyLjkzLC0xMS44MiAiLz4KICAgIDxwb2x5Z29uIGlkPSI1OCIgY2xhc3M9ImZpbDU4IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDIyLjY4LC0xMS43OCAyMy45MiwtMTEuOTQgIi8+CiAgICA8cG9seWdvbiBpZD0iNTkiIGNsYXNzPSJmaWw1OSIgcG9pbnRzPSIyOC45OSwyOC40OCAyMy42NywtMTEuOSAyNC45MSwtMTIuMDMgIi8+CiAgICA8cG9seWdvbiBpZD0iNjAiIGNsYXNzPSJmaWw2MCIgcG9pbnRzPSIyOC45OSwyOC40OCAyNC42NiwtMTIgMjUuOSwtMTIuMSAiLz4KICAgIDxwb2x5Z29uIGlkPSI2MSIgY2xhc3M9ImZpbDYxIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI1LjY1LC0xMi4wOCAyNi45LC0xMi4xNCAiLz4KICAgIDxwb2x5Z29uIGlkPSI2MiIgY2xhc3M9ImZpbDYyIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI2LjY1LC0xMi4xMyAyNy44OSwtMTIuMTYgIi8+CiAgICA8cG9seWdvbiBpZD0iNjMiIGNsYXNzPSJmaWw2MyIgcG9pbnRzPSIyOC45OSwyOC40OCAyNy42NCwtMTIuMTYgMjguODksLTEyLjE2ICIvPgogICAgPHBvbHlnb24gaWQ9IjY0IiBjbGFzcz0iZmlsNjQiIHBvaW50cz0iMjguOTksMjguNDggMjguNjQsLTEyLjE2IDI5Ljg5LC0xMi4xMyAiLz4KICAgIDxwb2x5Z29uIGlkPSI2NSIgY2xhc3M9ImZpbDY1IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI5LjY0LC0xMi4xNCAzMC44OSwtMTIuMDggIi8+CiAgICA8cG9seWdvbiBpZD0iNjYiIGNsYXNzPSJmaWw2NiIgcG9pbnRzPSIyOC45OSwyOC40OCAzMC42NCwtMTIuMDkgMzEuODgsLTEyICIvPgogICAgPHBvbHlnb24gaWQ9IjY3IiBjbGFzcz0iZmlsNjciIHBvaW50cz0iMjguOTksMjguNDggMzEuNjMsLTEyLjAyIDMyLjg4LC0xMS45ICIvPgogICAgPHBvbHlnb24gaWQ9IjY4IiBjbGFzcz0iZmlsNjgiIHBvaW50cz0iMjguOTksMjguNDggMzIuNjMsLTExLjkyIDMzLjg3LC0xMS43NyAiLz4KICAgIDxwb2x5Z29uIGlkPSI2OSIgY2xhc3M9ImZpbDY5IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDMzLjYyLC0xMS44IDM0Ljg2LC0xMS42MiAiLz4KICAgIDxwb2x5Z29uIGlkPSI3MCIgY2xhc3M9ImZpbDcwIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDM0LjYxLC0xMS42NiAzNS44NCwtMTEuNDUgIi8+CiAgICA8cG9seWdvbiBpZD0iNzEiIGNsYXNzPSJmaWw3MSIgcG9pbnRzPSIyOC45OSwyOC40OCAzNS42LC0xMS40OSAzNi44MiwtMTEuMjUgIi8+CiAgICA8cG9seWdvbiBpZD0iNzIiIGNsYXNzPSJmaWw3MiIgcG9pbnRzPSIyOC45OSwyOC40OCAzNi41OCwtMTEuMyAzNy44LC0xMS4wMyAiLz4KICAgIDxwb2x5Z29uIGlkPSI3MyIgY2xhc3M9ImZpbDczIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDM3LjU2LC0xMS4wOCAzOC43NywtMTAuNzggIi8+CiAgICA8cG9seWdvbiBpZD0iNzQiIGNsYXNzPSJmaWw3NCIgcG9pbnRzPSIyOC45OSwyOC40OCAzOC41MywtMTAuODQgMzkuNzQsLTEwLjUxICIvPgogICAgPHBvbHlnb24gaWQ9Ijc1IiBjbGFzcz0iZmlsNzUiIHBvaW50cz0iMjguOTksMjguNDggMzkuNSwtMTAuNTcgNDAuNywtMTAuMjIgIi8+CiAgICA8cG9seWdvbiBpZD0iNzYiIGNsYXNzPSJmaWw3NiIgcG9pbnRzPSIyOC45OSwyOC40OCA0MC40NiwtMTAuMjkgNDEuNjUsLTkuOSAiLz4KICAgIDxwb2x5Z29uIGlkPSI3NyIgY2xhc3M9ImZpbDc3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQxLjQxLC05Ljk4IDQyLjU5LC05LjU2ICIvPgogICAgPHBvbHlnb24gaWQ9Ijc4IiBjbGFzcz0iZmlsNzgiIHBvaW50cz0iMjguOTksMjguNDggNDIuMzYsLTkuNjQgNDMuNTMsLTkuMiAiLz4KICAgIDxwb2x5Z29uIGlkPSI3OSIgY2xhc3M9ImZpbDc5IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQzLjI5LC05LjI4IDQ0LjQ2LC04LjgxICIvPgogICAgPHBvbHlnb24gaWQ9IjgwIiBjbGFzcz0iZmlsODAiIHBvaW50cz0iMjguOTksMjguNDggNDQuMjIsLTguOTEgNDUuMzcsLTguNCAiLz4KICAgIDxwb2x5Z29uIGlkPSI4MSIgY2xhc3M9ImZpbDgxIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQ1LjE0LC04LjUgNDYuMjgsLTcuOTcgIi8+CiAgICA8cG9seWdvbiBpZD0iODIiIGNsYXNzPSJmaWw4MiIgcG9pbnRzPSIyOC45OSwyOC40OCA0Ni4wNSwtOC4wOCA0Ny4xOCwtNy41MiAiLz4KICAgIDxwb2x5Z29uIGlkPSI4MyIgY2xhc3M9ImZpbDgzIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQ2Ljk1LC03LjYzIDQ4LjA3LC03LjA1ICIvPgogICAgPHBvbHlnb24gaWQ9Ijg0IiBjbGFzcz0iZmlsODQiIHBvaW50cz0iMjguOTksMjguNDggNDcuODQsLTcuMTYgNDguOTQsLTYuNTUgIi8+CiAgICA8cG9seWdvbiBpZD0iODUiIGNsYXNzPSJmaWw4NSIgcG9pbnRzPSIyOC45OSwyOC40OCA0OC43MiwtNi42NyA0OS44LC02LjAzICIvPgogICAgPHBvbHlnb24gaWQ9Ijg2IiBjbGFzcz0iZmlsODYiIHBvaW50cz0iMjguOTksMjguNDggNDkuNTksLTYuMTYgNTAuNjUsLTUuNSAiLz4KICAgIDxwb2x5Z29uIGlkPSI4NyIgY2xhc3M9ImZpbDg3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDUwLjQ0LC01LjYzIDUxLjQ5LC00Ljk0ICIvPgogICAgPHBvbHlnb24gaWQ9Ijg4IiBjbGFzcz0iZmlsODgiIHBvaW50cz0iMjguOTksMjguNDggNTEuMjgsLTUuMDggNTIuMzIsLTQuMzYgIi8+CiAgICA8cG9seWdvbiBpZD0iODkiIGNsYXNzPSJmaWw4OSIgcG9pbnRzPSIyOC45OSwyOC40OCA1Mi4xMSwtNC41IDUzLjEzLC0zLjc2ICIvPgogICAgPHBvbHlnb24gaWQ9IjkwIiBjbGFzcz0iZmlsOTAiIHBvaW50cz0iMjguOTksMjguNDggNTIuOTIsLTMuOTEgNTMuOTIsLTMuMTUgIi8+CiAgICA8cG9seWdvbiBpZD0iOTEiIGNsYXNzPSJmaWw5MSIgcG9pbnRzPSIyOC45OSwyOC40OCA1My43MiwtMy4zIDU0LjcsLTIuNTEgIi8+CiAgICA8cG9seWdvbiBpZD0iOTIiIGNsYXNzPSJmaWw5MiIgcG9pbnRzPSIyOC45OSwyOC40OCA1NC41MSwtMi42NyA1NS40NywtMS44NiAiLz4KICAgIDxwb2x5Z29uIGlkPSI5MyIgY2xhc3M9ImZpbDkzIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDU1LjI4LC0yLjAyIDU2LjIyLC0xLjE4ICIvPgogICAgPHBvbHlnb24gaWQ9Ijk0IiBjbGFzcz0iZmlsOTQiIHBvaW50cz0iMjguOTksMjguNDggNTYuMDMsLTEuMzUgNTYuOTUsLTAuNDkgIi8+CiAgICA8cG9seWdvbiBpZD0iOTUiIGNsYXNzPSJmaWw5NSIgcG9pbnRzPSIyOC45OSwyOC40OCA1Ni43NiwtMC42NiA1Ny42NiwwLjIyICIvPgogICAgPHBvbHlnb24gaWQ9Ijk2IiBjbGFzcz0iZmlsOTYiIHBvaW50cz0iMjguOTksMjguNDggNTcuNDgsMC4wNCA1OC4zNiwwLjk0ICIvPgogICAgPHBvbHlnb24gaWQ9Ijk3IiBjbGFzcz0iZmlsOTciIHBvaW50cz0iMjguOTksMjguNDggNTguMTksMC43NiA1OS4wNCwxLjY4ICIvPgogICAgPHBvbHlnb24gaWQ9Ijk4IiBjbGFzcz0iZmlsOTgiIHBvaW50cz0iMjguOTksMjguNDggNTguODcsMS41IDU5LjcxLDIuNDQgIi8+CiAgICA8cG9seWdvbiBpZD0iOTkiIGNsYXNzPSJmaWw5OSIgcG9pbnRzPSIyOC45OSwyOC40OCA1OS41NCwyLjI1IDYwLjM1LDMuMjEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTAwIiBjbGFzcz0iZmlsMTAwIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDYwLjE5LDMuMDIgNjAuOTgsNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDEiIGNsYXNzPSJmaWwxMDEiIHBvaW50cz0iMjguOTksMjguNDggNjAuODIsMy44MSA2MS41OCw0LjgxICIvPgogICAgPHBvbHlnb24gaWQ9IjEwMiIgY2xhc3M9ImZpbDEwMiIgcG9pbnRzPSIyOC45OSwyOC40OCA2MS40Myw0LjYxIDYyLjE3LDUuNjIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTAzIiBjbGFzcz0iZmlsMTAzIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDYyLjAyLDUuNDIgNjIuNzMsNi40NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDQiIGNsYXNzPSJmaWwxMDQiIHBvaW50cz0iMjguOTksMjguNDggNjIuNTksNi4yNSA2My4yOCw3LjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTA1IiBjbGFzcz0iZmlsMTA1IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDYzLjE0LDcuMDkgNjMuODEsOC4xNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDYiIGNsYXNzPSJmaWwxMDYiIHBvaW50cz0iMjguOTksMjguNDggNjMuNjcsNy45NSA2NC4zMSw5LjAzICIvPgogICAgPHBvbHlnb24gaWQ9IjEwNyIgY2xhc3M9ImZpbDEwNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2NC4xOCw4LjgxIDY0Ljc5LDkuOTEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTA4IiBjbGFzcz0iZmlsMTA4IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY0LjY3LDkuNjkgNjUuMjYsMTAuOCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDkiIGNsYXNzPSJmaWwxMDkiIHBvaW50cz0iMjguOTksMjguNDggNjUuMTQsMTAuNTggNjUuNjksMTEuNzEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTEwIiBjbGFzcz0iZmlsMTEwIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY1LjU4LDExLjQ4IDY2LjExLDEyLjYyICIvPgogICAgPHBvbHlnb24gaWQ9IjExMSIgY2xhc3M9ImZpbDExMSIgcG9pbnRzPSIyOC45OSwyOC40OCA2Ni4wMSwxMi4zOSA2Ni41MSwxMy41NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMTIiIGNsYXNzPSJmaWwxMTIiIHBvaW50cz0iMjguOTksMjguNDggNjYuNDEsMTMuMzEgNjYuODgsMTQuNDggIi8+CiAgICA8cG9seWdvbiBpZD0iMTEzIiBjbGFzcz0iZmlsMTEzIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY2Ljc5LDE0LjI0IDY3LjIzLDE1LjQyICIvPgogICAgPHBvbHlnb24gaWQ9IjExNCIgY2xhc3M9ImZpbDExNCIgcG9pbnRzPSIyOC45OSwyOC40OCA2Ny4xNCwxNS4xOCA2Ny41NiwxNi4zNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMTUiIGNsYXNzPSJmaWwxMTUiIHBvaW50cz0iMjguOTksMjguNDggNjcuNDcsMTYuMTMgNjcuODYsMTcuMzIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTE2IiBjbGFzcz0iZmlsMTE2IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY3Ljc4LDE3LjA4IDY4LjE0LDE4LjI4ICIvPgogICAgPHBvbHlnb24gaWQ9IjExNyIgY2xhc3M9ImZpbDExNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2OC4wNywxOC4wNCA2OC40LDE5LjI1ICIvPgogICAgPHBvbHlnb24gaWQ9IjExOCIgY2xhc3M9ImZpbDExOCIgcG9pbnRzPSIyOC45OSwyOC40OCA2OC4zMywxOS4wMSA2OC42MywyMC4yMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMTkiIGNsYXNzPSJmaWwxMTkiIHBvaW50cz0iMjguOTksMjguNDggNjguNTcsMTkuOTggNjguODQsMjEuMiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjAiIGNsYXNzPSJmaWwxMjAiIHBvaW50cz0iMjguOTksMjguNDggNjguNzksMjAuOTYgNjkuMDIsMjIuMTkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTIxIiBjbGFzcz0iZmlsMTIxIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY4Ljk4LDIxLjk0IDY5LjE4LDIzLjE4ICIvPgogICAgPHBvbHlnb24gaWQ9IjEyMiIgY2xhc3M9ImZpbDEyMiIgcG9pbnRzPSIyOC45OSwyOC40OCA2OS4xNCwyMi45MyA2OS4zMiwyNC4xNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjMiIGNsYXNzPSJmaWwxMjMiIHBvaW50cz0iMjguOTksMjguNDggNjkuMjksMjMuOTIgNjkuNDMsMjUuMTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTI0IiBjbGFzcz0iZmlsMTI0IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY5LjQsMjQuOTEgNjkuNTIsMjYuMTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTI1IiBjbGFzcz0iZmlsMTI1IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY5LjUsMjUuOSA2OS41OSwyNy4xNSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjYiIGNsYXNzPSJmaWwxMjYiIHBvaW50cz0iMjguOTksMjguNDggNjkuNTcsMjYuOSA2OS42MiwyOC4xNSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjkuNjEsMjcuOSA2OS42NCwyOS4xNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjkuNjMsMjguOSA2OS42MywzMC4xNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjkuNjMsMjkuODkgNjkuNTksMzEuMTQgIi8+CiAgICA8cG9seWdvbiBpZD0iMTMwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY5LjYsMzAuODkgNjkuNTQsMzIuMTMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTMxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY5LjU1LDMxLjg4IDY5LjQ1LDMzLjEyICIvPgogICAgPHBvbHlnb24gaWQ9IjEzMiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2OS40NywzMi44OCA2OS4zNCwzNC4xMSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMzMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjkuMzcsMzMuODcgNjkuMjEsMzUuMSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMzQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjkuMjQsMzQuODUgNjkuMDYsMzYuMDggIi8+CiAgICA8cG9seWdvbiBpZD0iMTM1IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY5LjA5LDM1Ljg0IDY4Ljg4LDM3LjA2ICIvPgogICAgPHBvbHlnb24gaWQ9IjEzNiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2OC45MiwzNi44MSA2OC42NywzOC4wMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMzciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjguNzIsMzcuNzkgNjguNDQsMzkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTM4IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY4LjUsMzguNzYgNjguMTksMzkuOTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTM5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY4LjI1LDM5LjcyIDY3LjkyLDQwLjkxICIvPgogICAgPHBvbHlnb24gaWQ9IjE0MCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2Ny45OCw0MC42NyA2Ny42Miw0MS44NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDEiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjcuNjksNDEuNjIgNjcuMjksNDIuOCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjcuMzcsNDIuNTYgNjYuOTUsNDMuNzIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTQzIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY3LjAzLDQzLjQ5IDY2LjU4LDQ0LjY0ICIvPgogICAgPHBvbHlnb24gaWQ9IjE0NCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2Ni42Nyw0NC40MSA2Ni4xOSw0NS41NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjYuMjksNDUuMzMgNjUuNzgsNDYuNDUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTQ2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY1Ljg4LDQ2LjIzIDY1LjM0LDQ3LjM0ICIvPgogICAgPHBvbHlnb24gaWQ9IjE0NyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2NS40NSw0Ny4xMiA2NC44OCw0OC4yMiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjUsNDggNjQuNCw0OS4wOSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjQuNTIsNDguODcgNjMuOSw0OS45NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNTAiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjQuMDMsNDkuNzMgNjMuMzgsNTAuNzggIi8+CiAgICA8cG9seWdvbiBpZD0iMTUxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDYzLjUxLDUwLjU3IDYyLjg0LDUxLjYxICIvPgogICAgPHBvbHlnb24gaWQ9IjE1MiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2Mi45Nyw1MS40IDYyLjI4LDUyLjQyICIvPgogICAgPHBvbHlnb24gaWQ9IjE1MyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2Mi40Miw1Mi4yMiA2MS43LDUzLjIyICIvPgogICAgPHBvbHlnb24gaWQ9IjE1NCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2MS44NCw1My4wMiA2MS4wOSw1NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNTUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjEuMjQsNTMuODEgNjAuNDcsNTQuNzcgIi8+CiAgICA8cG9seWdvbiBpZD0iMTU2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDYwLjYzLDU0LjU4IDU5LjgzLDU1LjUyICIvPgogICAgPHBvbHlnb24gaWQ9IjE1NyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA1OS45OSw1NS4zNCA1OS4xNyw1Ni4yNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNTgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNTkuMzQsNTYuMDggNTguNDksNTYuOTggIi8+CiAgICA8cG9seWdvbiBpZD0iMTU5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDU4LjY2LDU2LjggNTcuOCw1Ny42OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNjAiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNTcuOTcsNTcuNTEgNTcuMDksNTguMzcgIi8+CiAgICA8cG9seWdvbiBpZD0iMTYxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDU3LjI2LDU4LjE5IDU2LjM2LDU5LjAzICIvPgogICAgPHBvbHlnb24gaWQ9IjE2MiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA1Ni41NCw1OC44NyA1NS42MSw1OS42OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNjMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNTUuOCw1OS41MiA1NC44NSw2MC4zMSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNjQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNTUuMDQsNjAuMTUgNTQuMDcsNjAuOTIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTY1IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDU0LjI3LDYwLjc3IDUzLjI4LDYxLjUxICIvPgogICAgPHBvbHlnb24gaWQ9IjE2NiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA1My40OCw2MS4zNiA1Mi40Nyw2Mi4wOCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNjciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNTIuNjcsNjEuOTQgNTEuNjUsNjIuNjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTY4IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDUxLjg2LDYyLjUgNTAuODIsNjMuMTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTY5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDUxLjAyLDYzLjAzIDQ5Ljk3LDYzLjY3ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3MCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA1MC4xOCw2My41NSA0OS4xMSw2NC4xNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNzEiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNDkuMzIsNjQuMDQgNDguMjMsNjQuNjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTcyIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQ4LjQ1LDY0LjUxIDQ3LjM1LDY1LjA3ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3MyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA0Ny41Nyw2NC45NiA0Ni40NSw2NS41ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3NCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA0Ni42OCw2NS4zOSA0NS41NSw2NS45ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3NSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA0NS43Nyw2NS43OSA0NC42Myw2Ni4yNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNzYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNDQuODYsNjYuMTggNDMuNzEsNjYuNjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTc3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQzLjk0LDY2LjU0IDQyLjc3LDY2Ljk2ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA0Myw2Ni44OCA0MS44Myw2Ny4yNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNzkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNDIuMDYsNjcuMTkgNDAuODgsNjcuNTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTgwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQxLjEyLDY3LjQ4IDM5LjkyLDY3LjgyICIvPgogICAgPHBvbHlnb24gaWQ9IjE4MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA0MC4xNiw2Ny43NSAzOC45Niw2OC4wNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMzkuMiw2OCAzNy45OSw2OC4yNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMzguMjMsNjguMjIgMzcuMDEsNjguNDYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTg0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDM3LjI1LDY4LjQxIDM2LjAzLDY4LjYzICIvPgogICAgPHBvbHlnb24gaWQ9IjE4NSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAzNi4yOCw2OC41OCAzNS4wNSw2OC43NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMzUuMjksNjguNzMgMzQuMDYsNjguODkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTg3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDM0LjMsNjguODYgMzMuMDcsNjguOTggIi8+CiAgICA8cG9seWdvbiBpZD0iMTg4IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDMzLjMxLDY4Ljk2IDMyLjA3LDY5LjA1ICIvPgogICAgPHBvbHlnb24gaWQ9IjE4OSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAzMi4zMiw2OS4wMyAzMS4wOCw2OS4xICIvPgogICAgPHBvbHlnb24gaWQ9IjE5MCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAzMS4zMyw2OS4wOCAzMC4wOCw2OS4xMiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOTEiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMzAuMzMsNjkuMTEgMjkuMDgsNjkuMTEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTkyIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI5LjMzLDY5LjExIDI4LjA4LDY5LjA4ICIvPgogICAgPHBvbHlnb24gaWQ9IjE5MyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAyOC4zMyw2OS4wOSAyNy4wOSw2OS4wMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOTQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMjcuMzQsNjkuMDQgMjYuMDksNjguOTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTk1IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI2LjM0LDY4Ljk3IDI1LjEsNjguODUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTk2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI1LjM1LDY4Ljg3IDI0LjEsNjguNzIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTk3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI0LjM1LDY4Ljc1IDIzLjEyLDY4LjU3ICIvPgogICAgPHBvbHlnb24gaWQ9IjE5OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAyMy4zNiw2OC42MSAyMi4xMyw2OC40ICIvPgogICAgPHBvbHlnb24gaWQ9IjE5OSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAyMi4zOCw2OC40NCAyMS4xNSw2OC4yICIvPgogICAgPHBvbHlnb24gaWQ9IjIwMCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAyMS4zOSw2OC4yNSAyMC4xNyw2Ny45OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDEiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMjAuNDIsNjguMDMgMTkuMiw2Ny43MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMTkuNDQsNjcuNzkgMTguMjQsNjcuNDYgIi8+CiAgICA8cG9seWdvbiBpZD0iMjAzIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDE4LjQ4LDY3LjUzIDE3LjI4LDY3LjE3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIwNCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAxNy41Miw2Ny4yNCAxNi4zMyw2Ni44NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMTYuNTYsNjYuOTMgMTUuMzgsNjYuNTEgIi8+CiAgICA8cG9seWdvbiBpZD0iMjA2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDE1LjYyLDY2LjU5IDE0LjQ0LDY2LjE1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIwNyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAxNC42OCw2Ni4yNCAxMy41Miw2NS43NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMTMuNzUsNjUuODYgMTIuNiw2NS4zNSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMTIuODMsNjUuNDYgMTEuNjksNjQuOTIgIi8+CiAgICA8cG9seWdvbiBpZD0iMjEwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDExLjkyLDY1LjAzIDEwLjc5LDY0LjQ3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxMSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAxMS4wMiw2NC41OCA5LjkxLDY0ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxMiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAxMC4xMyw2NC4xMiA5LjAzLDYzLjUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjEzIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDkuMjUsNjMuNjMgOC4xNyw2Mi45OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMTQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggOC4zOSw2My4xMSA3LjMyLDYyLjQ1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxNSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA3LjUzLDYyLjU4IDYuNDgsNjEuODkgIi8+CiAgICA8cG9seWdvbiBpZD0iMjE2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDYuNjksNjIuMDMgNS42Niw2MS4zMSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMTciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNS44Niw2MS40NiA0Ljg1LDYwLjcyICIvPgogICAgPHBvbHlnb24gaWQ9IjIxOCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA1LjA1LDYwLjg3IDQuMDUsNjAuMSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMTkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNC4yNSw2MC4yNSAzLjI3LDU5LjQ2ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyMCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAzLjQ3LDU5LjYyIDIuNTEsNTguODEgIi8+CiAgICA8cG9seWdvbiBpZD0iMjIxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDIuNyw1OC45NyAxLjc2LDU4LjE0ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyMiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAxLjk0LDU4LjMgMS4wMiw1Ny40NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMS4yMSw1Ny42MiAwLjMxLDU2Ljc0ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyNCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAwLjQ5LDU2LjkxIC0wLjM5LDU2LjAxICIvPgogICAgPHBvbHlnb24gaWQ9IjIyNSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtMC4yMSw1Ni4xOSAtMS4wNyw1NS4yNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTAuOSw1NS40NSAtMS43Myw1NC41MSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTEuNTcsNTQuNyAtMi4zOCw1My43NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTIuMjIsNTMuOTMgLTMsNTIuOTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjI5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0yLjg1LDUzLjE1IC0zLjYxLDUyLjE1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzMCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtMy40Niw1Mi4zNSAtNC4yLDUxLjMzICIvPgogICAgPHBvbHlnb24gaWQ9IjIzMSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtNC4wNSw1MS41MyAtNC43Niw1MC41ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzMiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtNC42Miw1MC43IC01LjMxLDQ5LjY1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzMyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtNS4xNyw0OS44NiAtNS44Myw0OC43OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMzQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTUuNyw0OS4wMSAtNi4zNCw0Ny45MiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMzUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTYuMjEsNDguMTQgLTYuODIsNDcuMDQgIi8+CiAgICA8cG9seWdvbiBpZD0iMjM2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC02LjcsNDcuMjYgLTcuMjgsNDYuMTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjM3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC03LjE3LDQ2LjM3IC03LjcyLDQ1LjI1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzOCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtNy42MSw0NS40NyAtOC4xNCw0NC4zMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMzkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTguMDMsNDQuNTYgLTguNTMsNDMuNDEgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC04LjQzLDQzLjY0IC04LjkxLDQyLjQ4ICIvPgogICAgPHBvbHlnb24gaWQ9IjI0MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtOC44MSw0Mi43MSAtOS4yNiw0MS41NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTkuMTcsNDEuNzcgLTkuNTgsNDAuNTkgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQzIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC05LjUsNDAuODIgLTkuODksMzkuNjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQ0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC05LjgxLDM5Ljg3IC0xMC4xNywzOC42NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTEwLjEsMzguOTEgLTEwLjQyLDM3LjcgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQ2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMC4zNiwzNy45NCAtMTAuNjYsMzYuNzMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQ3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMC42LDM2Ljk3IC0xMC44NywzNS43NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTEwLjgxLDM1Ljk5IC0xMS4wNSwzNC43NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTExLDM1LjAxIC0xMS4yMSwzMy43OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNTAiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTExLjE3LDM0LjAyIC0xMS4zNSwzMi43OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNTEiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTExLjMxLDMzLjAzIC0xMS40NiwzMS43OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNTIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTExLjQzLDMyLjA0IC0xMS41NSwzMC44ICIvPgogICAgPHBvbHlnb24gaWQ9IjI1MyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtMTEuNTIsMzEuMDUgLTExLjYxLDI5LjggIi8+CiAgICA8cG9seWdvbiBpZD0iMjU0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMS41OSwzMC4wNSAtMTEuNjUsMjguODEgIi8+CiAgICA8cG9seWdvbiBpZD0iMjU1IiBjbGFzcz0iZmlsMTI4IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMS42NCwyOS4wNSAtMTEuNjYsMjguMDYgIi8+CiAgIDwvZz4KICA8L2c+CiA8L2c+Cjwvc3ZnPg==") top no-repeat;
}
	html.theme-dark .large-2qn7A4BC .circleWrapper-2qn7A4BC{
        background-image:url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbDpzcGFjZT0icHJlc2VydmUiIHdpZHRoPSIzMTZweCIgaGVpZ2h0PSIxNThweCIgdmVyc2lvbj0iMS4xIiBzdHlsZT0ic2hhcGUtcmVuZGVyaW5nOmdlb21ldHJpY1ByZWNpc2lvbjsgdGV4dC1yZW5kZXJpbmc6Z2VvbWV0cmljUHJlY2lzaW9uOyBpbWFnZS1yZW5kZXJpbmc6b3B0aW1pemVRdWFsaXR5OyBmaWxsLXJ1bGU6ZXZlbm9kZDsgY2xpcC1ydWxlOmV2ZW5vZGQiCnZpZXdCb3g9IjAgMCA1Ny4wNiAyOC41MyIKIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIj4KIDxkZWZzPgogIDxzdHlsZSB0eXBlPSJ0ZXh0L2NzcyI+CiAgIDwhW0NEQVRBWwogICAgLmZpbDY0IHtmaWxsOiMwMEIyQzZ9CiAgICAuZmlsNjMge2ZpbGw6IzAwQjJDOH0KICAgIC5maWw2NyB7ZmlsbDojMDBCM0MwfQogICAgLmZpbDY2IHtmaWxsOiMwMEIzQzJ9CiAgICAuZmlsNjUge2ZpbGw6IzAwQjNDNH0KICAgIC5maWw3MCB7ZmlsbDojMDBCNEJCfQogICAgLmZpbDY5IHtmaWxsOiMwMEI0QkR9CiAgICAuZmlsNjgge2ZpbGw6IzAwQjRCRn0KICAgIC5maWw3MyB7ZmlsbDojMDBCNUI2fQogICAgLmZpbDcyIHtmaWxsOiMwMEI1Qjh9CiAgICAuZmlsNzEge2ZpbGw6IzAwQjVCOX0KICAgIC5maWw3NiB7ZmlsbDojMDBCNkIxfQogICAgLmZpbDc1IHtmaWxsOiMwMEI2QjJ9CiAgICAuZmlsNzQge2ZpbGw6IzAwQjZCNH0KICAgIC5maWw3OSB7ZmlsbDojMDBCN0FCfQogICAgLmZpbDc4IHtmaWxsOiMwMEI3QUR9CiAgICAuZmlsNzcge2ZpbGw6IzAwQjdBRn0KICAgIC5maWw4MiB7ZmlsbDojMDBCOEE2fQogICAgLmZpbDgxIHtmaWxsOiMwMEI4QTh9CiAgICAuZmlsODAge2ZpbGw6IzAwQjhBOX0KICAgIC5maWw4NSB7ZmlsbDojMDBCOUExfQogICAgLmZpbDg0IHtmaWxsOiMwMEI5QTJ9CiAgICAuZmlsODMge2ZpbGw6IzAwQjlBNH0KICAgIC5maWw4OCB7ZmlsbDojMDBCQTlCfQogICAgLmZpbDg3IHtmaWxsOiMwMEJBOUR9CiAgICAuZmlsODYge2ZpbGw6IzAwQkE5Rn0KICAgIC5maWw5MSB7ZmlsbDojMDBCQjk2fQogICAgLmZpbDkwIHtmaWxsOiMwMEJCOTh9CiAgICAuZmlsODkge2ZpbGw6IzAwQkI5OX0KICAgIC5maWw5NCB7ZmlsbDojMDBCQzkxfQogICAgLmZpbDkzIHtmaWxsOiMwMEJDOTJ9CiAgICAuZmlsOTIge2ZpbGw6IzAwQkM5NH0KICAgIC5maWw5NyB7ZmlsbDojMDBCRDhCfQogICAgLmZpbDk2IHtmaWxsOiMwMEJEOER9CiAgICAuZmlsOTUge2ZpbGw6IzAwQkQ4Rn0KICAgIC5maWwxMDAge2ZpbGw6IzAwQkU4Nn0KICAgIC5maWw5OSB7ZmlsbDojMDBCRTg4fQogICAgLmZpbDk4IHtmaWxsOiMwMEJFOEF9CiAgICAuZmlsMTAzIHtmaWxsOiMwMEJGODF9CiAgICAuZmlsMTAyIHtmaWxsOiMwMEJGODJ9CiAgICAuZmlsMTAxIHtmaWxsOiMwMEJGODR9CiAgICAuZmlsMTA2IHtmaWxsOiMwMEMwN0J9CiAgICAuZmlsMTA1IHtmaWxsOiMwMEMwN0R9CiAgICAuZmlsMTA0IHtmaWxsOiMwMEMwN0Z9CiAgICAuZmlsMTA5IHtmaWxsOiMwMEMxNzZ9CiAgICAuZmlsMTA4IHtmaWxsOiMwMEMxNzh9CiAgICAuZmlsMTA3IHtmaWxsOiMwMEMxN0F9CiAgICAuZmlsMTEyIHtmaWxsOiMwMEMyNzF9CiAgICAuZmlsMTExIHtmaWxsOiMwMEMyNzJ9CiAgICAuZmlsMTEwIHtmaWxsOiMwMEMyNzR9CiAgICAuZmlsMTE1IHtmaWxsOiMwMEMzNkJ9CiAgICAuZmlsMTE0IHtmaWxsOiMwMEMzNkR9CiAgICAuZmlsMTEzIHtmaWxsOiMwMEMzNkZ9CiAgICAuZmlsMTE4IHtmaWxsOiMwMEM0NjZ9CiAgICAuZmlsMTE3IHtmaWxsOiMwMEM0Njh9CiAgICAuZmlsMTE2IHtmaWxsOiMwMEM0NkF9CiAgICAuZmlsMTIxIHtmaWxsOiMwMEM1NjF9CiAgICAuZmlsMTIwIHtmaWxsOiMwMEM1NjN9CiAgICAuZmlsMTE5IHtmaWxsOiMwMEM1NjR9CiAgICAuZmlsMTI0IHtmaWxsOiMwMEM2NUJ9CiAgICAuZmlsMTIzIHtmaWxsOiMwMEM2NUR9CiAgICAuZmlsMTIyIHtmaWxsOiMwMEM2NUZ9CiAgICAuZmlsMTI3IHtmaWxsOiMwMEM3NTd9CiAgICAuZmlsMTI2IHtmaWxsOiMwMEM3NTh9CiAgICAuZmlsMTI1IHtmaWxsOiMwMEM3NUF9CiAgICAuZmlsNjIge2ZpbGw6IzAzQjBDNn0KICAgIC5maWw2MSB7ZmlsbDojMDdBREM0fQogICAgLmZpbDYwIHtmaWxsOiMwQkFBQzJ9CiAgICAuZmlsNTkge2ZpbGw6IzBGQThDMH0KICAgIC5maWw1OCB7ZmlsbDojMTNBNUJFfQogICAgLmZpbDU3IHtmaWxsOiMxN0EyQkN9CiAgICAuZmlsNTYge2ZpbGw6IzFCOUZCQX0KICAgIC5maWw1NSB7ZmlsbDojMUY5Q0I3fQogICAgLmZpbDU0IHtmaWxsOiMyMzlBQjV9CiAgICAuZmlsNTMge2ZpbGw6IzI3OTdCM30KICAgIC5maWw1MiB7ZmlsbDojMkI5NEIxfQogICAgLmZpbDUxIHtmaWxsOiMyRjkxQUZ9CiAgICAuZmlsNTAge2ZpbGw6IzMzOEVBRH0KICAgIC5maWw0OSB7ZmlsbDojMzc4Q0FCfQogICAgLmZpbDQ4IHtmaWxsOiMzQjg5QTl9CiAgICAuZmlsNDcge2ZpbGw6IzNGODZBNn0KICAgIC5maWw0NiB7ZmlsbDojNDM4M0E0fQogICAgLmZpbDQ1IHtmaWxsOiM0NzgwQTJ9CiAgICAuZmlsNDQge2ZpbGw6IzRCN0VBMH0KICAgIC5maWw0MyB7ZmlsbDojNEY3QjlFfQogICAgLmZpbDQyIHtmaWxsOiM1Mzc4OUN9CiAgICAuZmlsNDEge2ZpbGw6IzU3NzU5QX0KICAgIC5maWw0MCB7ZmlsbDojNUI3Mjk3fQogICAgLmZpbDM5IHtmaWxsOiM1RjcwOTV9CiAgICAuZmlsMzgge2ZpbGw6IzYzNkQ5M30KICAgIC5maWwzNyB7ZmlsbDojNjc2QTkxfQogICAgLmZpbDM2IHtmaWxsOiM2QjY3OEZ9CiAgICAuZmlsMzUge2ZpbGw6IzZGNjU4RH0KICAgIC5maWwzNCB7ZmlsbDojNzM2MjhCfQogICAgLmZpbDMzIHtmaWxsOiM3NzVGODl9CiAgICAuZmlsMzIge2ZpbGw6IzdCNUM4Nn0KICAgIC5maWwzMSB7ZmlsbDojN0Y1OTg0fQogICAgLmZpbDMwIHtmaWxsOiM4MzU3ODJ9CiAgICAuZmlsMjkge2ZpbGw6Izg3NTQ4MH0KICAgIC5maWwyOCB7ZmlsbDojOEI1MTdFfQogICAgLmZpbDI3IHtmaWxsOiM4RjRFN0N9CiAgICAuZmlsMjYge2ZpbGw6IzkzNEI3QX0KICAgIC5maWwyNSB7ZmlsbDojOTc0OTc3fQogICAgLmZpbDI0IHtmaWxsOiM5QjQ2NzV9CiAgICAuZmlsMjMge2ZpbGw6IzlGNDM3M30KICAgIC5maWwyMiB7ZmlsbDojQTM0MDcxfQogICAgLmZpbDIxIHtmaWxsOiNBNzNENkZ9CiAgICAuZmlsMjAge2ZpbGw6I0FCM0I2RH0KICAgIC5maWwxOSB7ZmlsbDojQUYzODZCfQogICAgLmZpbDE4IHtmaWxsOiNCMzM1Njl9CiAgICAuZmlsMTcge2ZpbGw6I0I3MzI2Nn0KICAgIC5maWwxNiB7ZmlsbDojQkIyRjY0fQogICAgLmZpbDE1IHtmaWxsOiNCRjJENjJ9CiAgICAuZmlsMTQge2ZpbGw6I0MzMkE2MH0KICAgIC5maWwxMyB7ZmlsbDojQzcyNzVFfQogICAgLmZpbDEyIHtmaWxsOiNDQjI0NUN9CiAgICAuZmlsMTEge2ZpbGw6I0NGMjI1QX0KICAgIC5maWwxMCB7ZmlsbDojRDMxRjU3fQogICAgLmZpbDkge2ZpbGw6I0Q3MUM1NX0KICAgIC5maWw4IHtmaWxsOiNEQjE5NTN9CiAgICAuZmlsNyB7ZmlsbDojREYxNjUxfQogICAgLmZpbDYge2ZpbGw6I0UzMTQ0Rn0KICAgIC5maWw1IHtmaWxsOiNFNzExNER9CiAgICAuZmlsNCB7ZmlsbDojRUIwRTRCfQogICAgLmZpbDMge2ZpbGw6I0VGMEI0OX0KICAgIC5maWwyIHtmaWxsOiNGMzA4NDZ9CiAgICAuZmlsMSB7ZmlsbDojRjcwNjQ0fQogICAgLmZpbDAge2ZpbGw6I0ZCMDM0Mn0KICAgIC5maWwxMjgge2ZpbGw6I0ZGMDA0MH0KICAgXV0+CiAgPC9zdHlsZT4KICAgIDxjbGlwUGF0aCBpZD0iaWQwIj4KICAgICA8cGF0aCBkPSJNNS4wMyAxMi4zNWMwLjA2LC0wLjA5IDAuMTcsLTAuMTUgMC4yOSwtMC4xNSAwLjA4LDAgMC4xNSwwLjAyIDAuMjEsMC4wNyAwLjE2LDAuMTEgMC4yLDAuMzQgMC4wOSwwLjUgLTMuMTMsNC41MyAtNC44NCw5LjkgLTQuOSwxNS40IDAsMC4yIC0wLjE2LDAuMzYgLTAuMzYsMC4zNiAtMC4yLDAgLTAuMzYsLTAuMTYgLTAuMzYsLTAuMzYgMCwwIDAsMCAwLDAgMC4wNywtNS44NyAxLjkyLC0xMS4zMSA1LjAzLC0xNS44MmwwIDB6bTQ2LjUgLTAuMDhjLTAuMDksMC4wNyAtMC4xNSwwLjE4IC0wLjE1LDAuMjkgMCwwLjA4IDAuMDIsMC4xNSAwLjA2LDAuMjEgMy4xMyw0LjUzIDQuODQsOS45IDQuOSwxNS40IDAsMC4yIDAuMTYsMC4zNiAwLjM2LDAuMzYgMC4yLDAgMC4zNiwtMC4xNiAwLjM2LC0wLjM2IDAsMCAwLDAgMCwwIC0wLjA1LC01LjY1IC0xLjgxLC0xMS4xNiAtNS4wMiwtMTUuODIgLTAuMDcsLTAuMDkgLTAuMTgsLTAuMTUgLTAuMywtMC4xNSAtMC4wNywwIC0wLjE1LDAuMDIgLTAuMjEsMC4wN2wwIDB6bS0xMy42MyAtOS45M2MtMC4xNSwtMC4wNSAtMC4yNCwtMC4xOSAtMC4yNCwtMC4zNCAwLC0wLjA0IDAsLTAuMDggMC4wMiwtMC4xMiAwLjA0LC0wLjE0IDAuMTgsLTAuMjQgMC4zNCwtMC4yNCAwLjA0LDAgMC4wOCwwIDAuMTEsMC4wMiA1LjE3LDEuODUgOS43MSw1LjE2IDEzLjA1LDkuNTIgMC4xMiwwLjE2IDAuMDksMC4zOSAtMC4wOCwwLjUgLTAuMDYsMC4wNSAtMC4xMywwLjA3IC0wLjIxLDAuMDcgLTAuMTEsMCAtMC4yMiwtMC4wNSAtMC4yOSwtMC4xNCAtMy4yNSwtNC4yNCAtNy42NywtNy40NiAtMTIuNywtOS4yN2wwIDB6bS0xNy44MyAtMC42OGMwLjA1LDAuMTUgMC4xOSwwLjI1IDAuMzUsMC4yNSAwLjAzLDAgMC4wNywtMC4wMSAwLjEsLTAuMDIgMi41OSwtMC43NyA1LjI4LC0xLjE3IDcuOTksLTEuMTcgMCwwIDAuMDEsMCAwLjAyLDAgMi43OCwwIDUuNDcsMC40MSA4LjAxLDEuMTcgMC4wMywwLjAxIDAuMDcsMC4wMiAwLjEsMC4wMiAwLjE2LDAgMC4zLC0wLjEgMC4zNSwtMC4yNSAwLjAxLC0wLjA0IDAuMDIsLTAuMDggMC4wMiwtMC4xMiAwLC0wLjE1IC0wLjExLC0wLjI5IC0wLjI2LC0wLjM0IC0yLjY1LC0wLjc5IC01LjQyLC0xLjIgLTguMTksLTEuMiAtMC4wMSwwIC0wLjAyLDAgLTAuMDMsMCAtMi44NiwwIC01LjYyLDAuNDIgLTguMjIsMS4yIC0wLjE1LDAuMDUgLTAuMjUsMC4xOSAtMC4yNSwwLjM0IDAsMC4wNCAwLDAuMDggMC4wMSwwLjEybDAgMHptLTAuNjggMC4yMmMwLjAxLDAuMDQgMC4wMiwwLjA4IDAuMDIsMC4xMiAwLDAuMTUgLTAuMSwwLjI5IC0wLjI1LDAuMzQgLTUuMDMsMS44IC05LjQ1LDUuMDMgLTEyLjcsOS4yNyAtMC4wNywwLjA5IC0wLjE4LDAuMTQgLTAuMjksMC4xNCAtMC4wOCwwIC0wLjE1LC0wLjAyIC0wLjIxLC0wLjA3IC0wLjEsLTAuMDYgLTAuMTUsLTAuMTcgLTAuMTUsLTAuMjkgMCwtMC4wNyAwLjAzLC0wLjE1IDAuMDcsLTAuMjEgMy4zNCwtNC4zNiA3Ljg4LC03LjY3IDEzLjA1LC05LjUyIDAuMTksLTAuMDcgMC4zOSwwLjAzIDAuNDYsMC4yMmwwIDB6Ii8+CiAgICA8L2NsaXBQYXRoPgogPC9kZWZzPgogPGcgaWQ9IjEiPgogIDxnPgogICA8ZyBzdHlsZT0iY2xpcC1wYXRoOnVybCgjaWQwKSI+CiAgICA8cG9seWdvbiBjbGFzcz0iZmlsMCIgcG9pbnRzPSIyOC45OSwyOC40OCAtMTEuNjYsMjguMzEgLTExLjY2LDI2LjgxICIvPgogICAgPHBvbHlnb24gaWQ9IjEiIGNsYXNzPSJmaWwxIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMS42NiwyNy4wNiAtMTEuNjIsMjUuODEgIi8+CiAgICA8cG9seWdvbiBpZD0iMiIgY2xhc3M9ImZpbDIiIHBvaW50cz0iMjguOTksMjguNDggLTExLjYzLDI2LjA2IC0xMS41NiwyNC44MiAiLz4KICAgIDxwb2x5Z29uIGlkPSIzIiBjbGFzcz0iZmlsMyIgcG9pbnRzPSIyOC45OSwyOC40OCAtMTEuNTgsMjUuMDcgLTExLjQ4LDIzLjgzICIvPgogICAgPHBvbHlnb24gaWQ9IjQiIGNsYXNzPSJmaWw0IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMS41LDI0LjA4IC0xMS4zNywyMi44NCAiLz4KICAgIDxwb2x5Z29uIGlkPSI1IiBjbGFzcz0iZmlsNSIgcG9pbnRzPSIyOC45OSwyOC40OCAtMTEuNCwyMy4wOSAtMTEuMjQsMjEuODUgIi8+CiAgICA8cG9seWdvbiBpZD0iNiIgY2xhc3M9ImZpbDYiIHBvaW50cz0iMjguOTksMjguNDggLTExLjI3LDIyLjEgLTExLjA4LDIwLjg3ICIvPgogICAgPHBvbHlnb24gaWQ9IjciIGNsYXNzPSJmaWw3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMS4xMiwyMS4xMiAtMTAuOSwxOS44OSAiLz4KICAgIDxwb2x5Z29uIGlkPSI4IiBjbGFzcz0iZmlsOCIgcG9pbnRzPSIyOC45OSwyOC40OCAtMTAuOTUsMjAuMTQgLTEwLjcsMTguOTIgIi8+CiAgICA8cG9seWdvbiBpZD0iOSIgY2xhc3M9ImZpbDkiIHBvaW50cz0iMjguOTksMjguNDggLTEwLjc1LDE5LjE2IC0xMC40NywxNy45NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMCIgY2xhc3M9ImZpbDEwIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMC41MywxOC4yIC0xMC4yMiwxNi45OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMSIgY2xhc3M9ImZpbDExIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMC4yOCwxNy4yMyAtOS45NCwxNi4wNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMiIgY2xhc3M9ImZpbDEyIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMC4wMSwxNi4yOCAtOS42NCwxNS4xICIvPgogICAgPHBvbHlnb24gaWQ9IjEzIiBjbGFzcz0iZmlsMTMiIHBvaW50cz0iMjguOTksMjguNDggLTkuNzIsMTUuMzMgLTkuMzIsMTQuMTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTQiIGNsYXNzPSJmaWwxNCIgcG9pbnRzPSIyOC45OSwyOC40OCAtOS40LDE0LjM5IC04Ljk4LDEzLjIzICIvPgogICAgPHBvbHlnb24gaWQ9IjE1IiBjbGFzcz0iZmlsMTUiIHBvaW50cz0iMjguOTksMjguNDggLTkuMDYsMTMuNDYgLTguNjEsMTIuMzEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTYiIGNsYXNzPSJmaWwxNiIgcG9pbnRzPSIyOC45OSwyOC40OCAtOC43LDEyLjU0IC04LjIyLDExLjQgIi8+CiAgICA8cG9seWdvbiBpZD0iMTciIGNsYXNzPSJmaWwxNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtOC4zMSwxMS42MyAtNy44LDEwLjUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTgiIGNsYXNzPSJmaWwxOCIgcG9pbnRzPSIyOC45OSwyOC40OCAtNy45MSwxMC43MiAtNy4zNyw5LjYxICIvPgogICAgPHBvbHlnb24gaWQ9IjE5IiBjbGFzcz0iZmlsMTkiIHBvaW50cz0iMjguOTksMjguNDggLTcuNDgsOS44MyAtNi45MSw4LjczICIvPgogICAgPHBvbHlnb24gaWQ9IjIwIiBjbGFzcz0iZmlsMjAiIHBvaW50cz0iMjguOTksMjguNDggLTcuMDIsOC45NSAtNi40Myw3Ljg3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxIiBjbGFzcz0iZmlsMjEiIHBvaW50cz0iMjguOTksMjguNDggLTYuNTUsOC4wOCAtNS45Myw3LjAxICIvPgogICAgPHBvbHlnb24gaWQ9IjIyIiBjbGFzcz0iZmlsMjIiIHBvaW50cz0iMjguOTksMjguNDggLTYuMDUsNy4yMyAtNS40MSw2LjE3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzIiBjbGFzcz0iZmlsMjMiIHBvaW50cz0iMjguOTksMjguNDggLTUuNTQsNi4zOCAtNC44Nyw1LjM0ICIvPgogICAgPHBvbHlnb24gaWQ9IjI0IiBjbGFzcz0iZmlsMjQiIHBvaW50cz0iMjguOTksMjguNDggLTUsNS41NSAtNC4zLDQuNTMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjUiIGNsYXNzPSJmaWwyNSIgcG9pbnRzPSIyOC45OSwyOC40OCAtNC40NCw0Ljc0IC0zLjcyLDMuNzMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjYiIGNsYXNzPSJmaWwyNiIgcG9pbnRzPSIyOC45OSwyOC40OCAtMy44NywzLjkzIC0zLjEyLDIuOTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjciIGNsYXNzPSJmaWwyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtMy4yNywzLjE1IC0yLjUsMi4xOCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyOCIgY2xhc3M9ImZpbDI4IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0yLjY1LDIuMzcgLTEuODYsMS40MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyOSIgY2xhc3M9ImZpbDI5IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0yLjAyLDEuNjIgLTEuMiwwLjY5ICIvPgogICAgPHBvbHlnb24gaWQ9IjMwIiBjbGFzcz0iZmlsMzAiIHBvaW50cz0iMjguOTksMjguNDggLTEuMzYsMC44OCAtMC41MiwtMC4wMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIzMSIgY2xhc3M9ImZpbDMxIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0wLjY5LDAuMTUgMC4xNywtMC43MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIzMiIgY2xhc3M9ImZpbDMyIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDAsLTAuNTUgMC44OSwtMS40MSAiLz4KICAgIDxwb2x5Z29uIGlkPSIzMyIgY2xhc3M9ImZpbDMzIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDAuNzEsLTEuMjQgMS42MiwtMi4wOCAiLz4KICAgIDxwb2x5Z29uIGlkPSIzNCIgY2xhc3M9ImZpbDM0IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDEuNDMsLTEuOTEgMi4zNiwtMi43MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIzNSIgY2xhc3M9ImZpbDM1IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDIuMTgsLTIuNTcgMy4xMiwtMy4zNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIzNiIgY2xhc3M9ImZpbDM2IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDIuOTMsLTMuMiAzLjksLTMuOTcgIi8+CiAgICA8cG9seWdvbiBpZD0iMzciIGNsYXNzPSJmaWwzNyIgcG9pbnRzPSIyOC45OSwyOC40OCAzLjcxLC0zLjgyIDQuNjksLTQuNTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMzgiIGNsYXNzPSJmaWwzOCIgcG9pbnRzPSIyOC45OSwyOC40OCA0LjUsLTQuNDEgNS41LC01LjEzICIvPgogICAgPHBvbHlnb24gaWQ9IjM5IiBjbGFzcz0iZmlsMzkiIHBvaW50cz0iMjguOTksMjguNDggNS4zLC00Ljk5IDYuMzIsLTUuNjggIi8+CiAgICA8cG9seWdvbiBpZD0iNDAiIGNsYXNzPSJmaWw0MCIgcG9pbnRzPSIyOC45OSwyOC40OCA2LjEyLC01LjU0IDcuMTYsLTYuMjEgIi8+CiAgICA8cG9seWdvbiBpZD0iNDEiIGNsYXNzPSJmaWw0MSIgcG9pbnRzPSIyOC45OSwyOC40OCA2Ljk1LC02LjA4IDguMDEsLTYuNzIgIi8+CiAgICA8cG9seWdvbiBpZD0iNDIiIGNsYXNzPSJmaWw0MiIgcG9pbnRzPSIyOC45OSwyOC40OCA3Ljc5LC02LjU5IDguODcsLTcuMjEgIi8+CiAgICA8cG9seWdvbiBpZD0iNDMiIGNsYXNzPSJmaWw0MyIgcG9pbnRzPSIyOC45OSwyOC40OCA4LjY1LC03LjA5IDkuNzQsLTcuNjggIi8+CiAgICA8cG9seWdvbiBpZD0iNDQiIGNsYXNzPSJmaWw0NCIgcG9pbnRzPSIyOC45OSwyOC40OCA5LjUyLC03LjU2IDEwLjYyLC04LjEyICIvPgogICAgPHBvbHlnb24gaWQ9IjQ1IiBjbGFzcz0iZmlsNDUiIHBvaW50cz0iMjguOTksMjguNDggMTAuNCwtOC4wMSAxMS41MiwtOC41NCAiLz4KICAgIDxwb2x5Z29uIGlkPSI0NiIgY2xhc3M9ImZpbDQ2IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDExLjMsLTguNDQgMTIuNDMsLTguOTQgIi8+CiAgICA8cG9seWdvbiBpZD0iNDciIGNsYXNzPSJmaWw0NyIgcG9pbnRzPSIyOC45OSwyOC40OCAxMi4yLC04Ljg0IDEzLjM0LC05LjMyICIvPgogICAgPHBvbHlnb24gaWQ9IjQ4IiBjbGFzcz0iZmlsNDgiIHBvaW50cz0iMjguOTksMjguNDggMTMuMTEsLTkuMjMgMTQuMjcsLTkuNjggIi8+CiAgICA8cG9seWdvbiBpZD0iNDkiIGNsYXNzPSJmaWw0OSIgcG9pbnRzPSIyOC45OSwyOC40OCAxNC4wNCwtOS41OSAxNS4yLC0xMC4wMSAiLz4KICAgIDxwb2x5Z29uIGlkPSI1MCIgY2xhc3M9ImZpbDUwIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDE0Ljk3LC05LjkyIDE2LjE0LC0xMC4zMiAiLz4KICAgIDxwb2x5Z29uIGlkPSI1MSIgY2xhc3M9ImZpbDUxIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDE1LjkxLC0xMC4yNCAxNy4wOSwtMTAuNiAiLz4KICAgIDxwb2x5Z29uIGlkPSI1MiIgY2xhc3M9ImZpbDUyIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDE2Ljg2LC0xMC41MyAxOC4wNSwtMTAuODcgIi8+CiAgICA8cG9seWdvbiBpZD0iNTMiIGNsYXNzPSJmaWw1MyIgcG9pbnRzPSIyOC45OSwyOC40OCAxNy44MSwtMTAuOCAxOS4wMiwtMTEuMSAiLz4KICAgIDxwb2x5Z29uIGlkPSI1NCIgY2xhc3M9ImZpbDU0IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDE4Ljc4LC0xMS4wNCAxOS45OSwtMTEuMzIgIi8+CiAgICA8cG9seWdvbiBpZD0iNTUiIGNsYXNzPSJmaWw1NSIgcG9pbnRzPSIyOC45OSwyOC40OCAxOS43NCwtMTEuMjYgMjAuOTYsLTExLjUxICIvPgogICAgPHBvbHlnb24gaWQ9IjU2IiBjbGFzcz0iZmlsNTYiIHBvaW50cz0iMjguOTksMjguNDggMjAuNzIsLTExLjQ2IDIxLjk0LC0xMS42OCAiLz4KICAgIDxwb2x5Z29uIGlkPSI1NyIgY2xhc3M9ImZpbDU3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDIxLjcsLTExLjYzIDIyLjkzLC0xMS44MiAiLz4KICAgIDxwb2x5Z29uIGlkPSI1OCIgY2xhc3M9ImZpbDU4IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDIyLjY4LC0xMS43OCAyMy45MiwtMTEuOTQgIi8+CiAgICA8cG9seWdvbiBpZD0iNTkiIGNsYXNzPSJmaWw1OSIgcG9pbnRzPSIyOC45OSwyOC40OCAyMy42NywtMTEuOSAyNC45MSwtMTIuMDMgIi8+CiAgICA8cG9seWdvbiBpZD0iNjAiIGNsYXNzPSJmaWw2MCIgcG9pbnRzPSIyOC45OSwyOC40OCAyNC42NiwtMTIgMjUuOSwtMTIuMSAiLz4KICAgIDxwb2x5Z29uIGlkPSI2MSIgY2xhc3M9ImZpbDYxIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI1LjY1LC0xMi4wOCAyNi45LC0xMi4xNCAiLz4KICAgIDxwb2x5Z29uIGlkPSI2MiIgY2xhc3M9ImZpbDYyIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI2LjY1LC0xMi4xMyAyNy44OSwtMTIuMTYgIi8+CiAgICA8cG9seWdvbiBpZD0iNjMiIGNsYXNzPSJmaWw2MyIgcG9pbnRzPSIyOC45OSwyOC40OCAyNy42NCwtMTIuMTYgMjguODksLTEyLjE2ICIvPgogICAgPHBvbHlnb24gaWQ9IjY0IiBjbGFzcz0iZmlsNjQiIHBvaW50cz0iMjguOTksMjguNDggMjguNjQsLTEyLjE2IDI5Ljg5LC0xMi4xMyAiLz4KICAgIDxwb2x5Z29uIGlkPSI2NSIgY2xhc3M9ImZpbDY1IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI5LjY0LC0xMi4xNCAzMC44OSwtMTIuMDggIi8+CiAgICA8cG9seWdvbiBpZD0iNjYiIGNsYXNzPSJmaWw2NiIgcG9pbnRzPSIyOC45OSwyOC40OCAzMC42NCwtMTIuMDkgMzEuODgsLTEyICIvPgogICAgPHBvbHlnb24gaWQ9IjY3IiBjbGFzcz0iZmlsNjciIHBvaW50cz0iMjguOTksMjguNDggMzEuNjMsLTEyLjAyIDMyLjg4LC0xMS45ICIvPgogICAgPHBvbHlnb24gaWQ9IjY4IiBjbGFzcz0iZmlsNjgiIHBvaW50cz0iMjguOTksMjguNDggMzIuNjMsLTExLjkyIDMzLjg3LC0xMS43NyAiLz4KICAgIDxwb2x5Z29uIGlkPSI2OSIgY2xhc3M9ImZpbDY5IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDMzLjYyLC0xMS44IDM0Ljg2LC0xMS42MiAiLz4KICAgIDxwb2x5Z29uIGlkPSI3MCIgY2xhc3M9ImZpbDcwIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDM0LjYxLC0xMS42NiAzNS44NCwtMTEuNDUgIi8+CiAgICA8cG9seWdvbiBpZD0iNzEiIGNsYXNzPSJmaWw3MSIgcG9pbnRzPSIyOC45OSwyOC40OCAzNS42LC0xMS40OSAzNi44MiwtMTEuMjUgIi8+CiAgICA8cG9seWdvbiBpZD0iNzIiIGNsYXNzPSJmaWw3MiIgcG9pbnRzPSIyOC45OSwyOC40OCAzNi41OCwtMTEuMyAzNy44LC0xMS4wMyAiLz4KICAgIDxwb2x5Z29uIGlkPSI3MyIgY2xhc3M9ImZpbDczIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDM3LjU2LC0xMS4wOCAzOC43NywtMTAuNzggIi8+CiAgICA8cG9seWdvbiBpZD0iNzQiIGNsYXNzPSJmaWw3NCIgcG9pbnRzPSIyOC45OSwyOC40OCAzOC41MywtMTAuODQgMzkuNzQsLTEwLjUxICIvPgogICAgPHBvbHlnb24gaWQ9Ijc1IiBjbGFzcz0iZmlsNzUiIHBvaW50cz0iMjguOTksMjguNDggMzkuNSwtMTAuNTcgNDAuNywtMTAuMjIgIi8+CiAgICA8cG9seWdvbiBpZD0iNzYiIGNsYXNzPSJmaWw3NiIgcG9pbnRzPSIyOC45OSwyOC40OCA0MC40NiwtMTAuMjkgNDEuNjUsLTkuOSAiLz4KICAgIDxwb2x5Z29uIGlkPSI3NyIgY2xhc3M9ImZpbDc3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQxLjQxLC05Ljk4IDQyLjU5LC05LjU2ICIvPgogICAgPHBvbHlnb24gaWQ9Ijc4IiBjbGFzcz0iZmlsNzgiIHBvaW50cz0iMjguOTksMjguNDggNDIuMzYsLTkuNjQgNDMuNTMsLTkuMiAiLz4KICAgIDxwb2x5Z29uIGlkPSI3OSIgY2xhc3M9ImZpbDc5IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQzLjI5LC05LjI4IDQ0LjQ2LC04LjgxICIvPgogICAgPHBvbHlnb24gaWQ9IjgwIiBjbGFzcz0iZmlsODAiIHBvaW50cz0iMjguOTksMjguNDggNDQuMjIsLTguOTEgNDUuMzcsLTguNCAiLz4KICAgIDxwb2x5Z29uIGlkPSI4MSIgY2xhc3M9ImZpbDgxIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQ1LjE0LC04LjUgNDYuMjgsLTcuOTcgIi8+CiAgICA8cG9seWdvbiBpZD0iODIiIGNsYXNzPSJmaWw4MiIgcG9pbnRzPSIyOC45OSwyOC40OCA0Ni4wNSwtOC4wOCA0Ny4xOCwtNy41MiAiLz4KICAgIDxwb2x5Z29uIGlkPSI4MyIgY2xhc3M9ImZpbDgzIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQ2Ljk1LC03LjYzIDQ4LjA3LC03LjA1ICIvPgogICAgPHBvbHlnb24gaWQ9Ijg0IiBjbGFzcz0iZmlsODQiIHBvaW50cz0iMjguOTksMjguNDggNDcuODQsLTcuMTYgNDguOTQsLTYuNTUgIi8+CiAgICA8cG9seWdvbiBpZD0iODUiIGNsYXNzPSJmaWw4NSIgcG9pbnRzPSIyOC45OSwyOC40OCA0OC43MiwtNi42NyA0OS44LC02LjAzICIvPgogICAgPHBvbHlnb24gaWQ9Ijg2IiBjbGFzcz0iZmlsODYiIHBvaW50cz0iMjguOTksMjguNDggNDkuNTksLTYuMTYgNTAuNjUsLTUuNSAiLz4KICAgIDxwb2x5Z29uIGlkPSI4NyIgY2xhc3M9ImZpbDg3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDUwLjQ0LC01LjYzIDUxLjQ5LC00Ljk0ICIvPgogICAgPHBvbHlnb24gaWQ9Ijg4IiBjbGFzcz0iZmlsODgiIHBvaW50cz0iMjguOTksMjguNDggNTEuMjgsLTUuMDggNTIuMzIsLTQuMzYgIi8+CiAgICA8cG9seWdvbiBpZD0iODkiIGNsYXNzPSJmaWw4OSIgcG9pbnRzPSIyOC45OSwyOC40OCA1Mi4xMSwtNC41IDUzLjEzLC0zLjc2ICIvPgogICAgPHBvbHlnb24gaWQ9IjkwIiBjbGFzcz0iZmlsOTAiIHBvaW50cz0iMjguOTksMjguNDggNTIuOTIsLTMuOTEgNTMuOTIsLTMuMTUgIi8+CiAgICA8cG9seWdvbiBpZD0iOTEiIGNsYXNzPSJmaWw5MSIgcG9pbnRzPSIyOC45OSwyOC40OCA1My43MiwtMy4zIDU0LjcsLTIuNTEgIi8+CiAgICA8cG9seWdvbiBpZD0iOTIiIGNsYXNzPSJmaWw5MiIgcG9pbnRzPSIyOC45OSwyOC40OCA1NC41MSwtMi42NyA1NS40NywtMS44NiAiLz4KICAgIDxwb2x5Z29uIGlkPSI5MyIgY2xhc3M9ImZpbDkzIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDU1LjI4LC0yLjAyIDU2LjIyLC0xLjE4ICIvPgogICAgPHBvbHlnb24gaWQ9Ijk0IiBjbGFzcz0iZmlsOTQiIHBvaW50cz0iMjguOTksMjguNDggNTYuMDMsLTEuMzUgNTYuOTUsLTAuNDkgIi8+CiAgICA8cG9seWdvbiBpZD0iOTUiIGNsYXNzPSJmaWw5NSIgcG9pbnRzPSIyOC45OSwyOC40OCA1Ni43NiwtMC42NiA1Ny42NiwwLjIyICIvPgogICAgPHBvbHlnb24gaWQ9Ijk2IiBjbGFzcz0iZmlsOTYiIHBvaW50cz0iMjguOTksMjguNDggNTcuNDgsMC4wNCA1OC4zNiwwLjk0ICIvPgogICAgPHBvbHlnb24gaWQ9Ijk3IiBjbGFzcz0iZmlsOTciIHBvaW50cz0iMjguOTksMjguNDggNTguMTksMC43NiA1OS4wNCwxLjY4ICIvPgogICAgPHBvbHlnb24gaWQ9Ijk4IiBjbGFzcz0iZmlsOTgiIHBvaW50cz0iMjguOTksMjguNDggNTguODcsMS41IDU5LjcxLDIuNDQgIi8+CiAgICA8cG9seWdvbiBpZD0iOTkiIGNsYXNzPSJmaWw5OSIgcG9pbnRzPSIyOC45OSwyOC40OCA1OS41NCwyLjI1IDYwLjM1LDMuMjEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTAwIiBjbGFzcz0iZmlsMTAwIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDYwLjE5LDMuMDIgNjAuOTgsNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDEiIGNsYXNzPSJmaWwxMDEiIHBvaW50cz0iMjguOTksMjguNDggNjAuODIsMy44MSA2MS41OCw0LjgxICIvPgogICAgPHBvbHlnb24gaWQ9IjEwMiIgY2xhc3M9ImZpbDEwMiIgcG9pbnRzPSIyOC45OSwyOC40OCA2MS40Myw0LjYxIDYyLjE3LDUuNjIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTAzIiBjbGFzcz0iZmlsMTAzIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDYyLjAyLDUuNDIgNjIuNzMsNi40NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDQiIGNsYXNzPSJmaWwxMDQiIHBvaW50cz0iMjguOTksMjguNDggNjIuNTksNi4yNSA2My4yOCw3LjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTA1IiBjbGFzcz0iZmlsMTA1IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDYzLjE0LDcuMDkgNjMuODEsOC4xNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDYiIGNsYXNzPSJmaWwxMDYiIHBvaW50cz0iMjguOTksMjguNDggNjMuNjcsNy45NSA2NC4zMSw5LjAzICIvPgogICAgPHBvbHlnb24gaWQ9IjEwNyIgY2xhc3M9ImZpbDEwNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2NC4xOCw4LjgxIDY0Ljc5LDkuOTEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTA4IiBjbGFzcz0iZmlsMTA4IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY0LjY3LDkuNjkgNjUuMjYsMTAuOCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDkiIGNsYXNzPSJmaWwxMDkiIHBvaW50cz0iMjguOTksMjguNDggNjUuMTQsMTAuNTggNjUuNjksMTEuNzEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTEwIiBjbGFzcz0iZmlsMTEwIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY1LjU4LDExLjQ4IDY2LjExLDEyLjYyICIvPgogICAgPHBvbHlnb24gaWQ9IjExMSIgY2xhc3M9ImZpbDExMSIgcG9pbnRzPSIyOC45OSwyOC40OCA2Ni4wMSwxMi4zOSA2Ni41MSwxMy41NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMTIiIGNsYXNzPSJmaWwxMTIiIHBvaW50cz0iMjguOTksMjguNDggNjYuNDEsMTMuMzEgNjYuODgsMTQuNDggIi8+CiAgICA8cG9seWdvbiBpZD0iMTEzIiBjbGFzcz0iZmlsMTEzIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY2Ljc5LDE0LjI0IDY3LjIzLDE1LjQyICIvPgogICAgPHBvbHlnb24gaWQ9IjExNCIgY2xhc3M9ImZpbDExNCIgcG9pbnRzPSIyOC45OSwyOC40OCA2Ny4xNCwxNS4xOCA2Ny41NiwxNi4zNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMTUiIGNsYXNzPSJmaWwxMTUiIHBvaW50cz0iMjguOTksMjguNDggNjcuNDcsMTYuMTMgNjcuODYsMTcuMzIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTE2IiBjbGFzcz0iZmlsMTE2IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY3Ljc4LDE3LjA4IDY4LjE0LDE4LjI4ICIvPgogICAgPHBvbHlnb24gaWQ9IjExNyIgY2xhc3M9ImZpbDExNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2OC4wNywxOC4wNCA2OC40LDE5LjI1ICIvPgogICAgPHBvbHlnb24gaWQ9IjExOCIgY2xhc3M9ImZpbDExOCIgcG9pbnRzPSIyOC45OSwyOC40OCA2OC4zMywxOS4wMSA2OC42MywyMC4yMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMTkiIGNsYXNzPSJmaWwxMTkiIHBvaW50cz0iMjguOTksMjguNDggNjguNTcsMTkuOTggNjguODQsMjEuMiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjAiIGNsYXNzPSJmaWwxMjAiIHBvaW50cz0iMjguOTksMjguNDggNjguNzksMjAuOTYgNjkuMDIsMjIuMTkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTIxIiBjbGFzcz0iZmlsMTIxIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY4Ljk4LDIxLjk0IDY5LjE4LDIzLjE4ICIvPgogICAgPHBvbHlnb24gaWQ9IjEyMiIgY2xhc3M9ImZpbDEyMiIgcG9pbnRzPSIyOC45OSwyOC40OCA2OS4xNCwyMi45MyA2OS4zMiwyNC4xNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjMiIGNsYXNzPSJmaWwxMjMiIHBvaW50cz0iMjguOTksMjguNDggNjkuMjksMjMuOTIgNjkuNDMsMjUuMTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTI0IiBjbGFzcz0iZmlsMTI0IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY5LjQsMjQuOTEgNjkuNTIsMjYuMTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTI1IiBjbGFzcz0iZmlsMTI1IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY5LjUsMjUuOSA2OS41OSwyNy4xNSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjYiIGNsYXNzPSJmaWwxMjYiIHBvaW50cz0iMjguOTksMjguNDggNjkuNTcsMjYuOSA2OS42MiwyOC4xNSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjkuNjEsMjcuOSA2OS42NCwyOS4xNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjkuNjMsMjguOSA2OS42MywzMC4xNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjkuNjMsMjkuODkgNjkuNTksMzEuMTQgIi8+CiAgICA8cG9seWdvbiBpZD0iMTMwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY5LjYsMzAuODkgNjkuNTQsMzIuMTMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTMxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY5LjU1LDMxLjg4IDY5LjQ1LDMzLjEyICIvPgogICAgPHBvbHlnb24gaWQ9IjEzMiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2OS40NywzMi44OCA2OS4zNCwzNC4xMSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMzMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjkuMzcsMzMuODcgNjkuMjEsMzUuMSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMzQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjkuMjQsMzQuODUgNjkuMDYsMzYuMDggIi8+CiAgICA8cG9seWdvbiBpZD0iMTM1IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY5LjA5LDM1Ljg0IDY4Ljg4LDM3LjA2ICIvPgogICAgPHBvbHlnb24gaWQ9IjEzNiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2OC45MiwzNi44MSA2OC42NywzOC4wMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMzciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjguNzIsMzcuNzkgNjguNDQsMzkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTM4IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY4LjUsMzguNzYgNjguMTksMzkuOTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTM5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY4LjI1LDM5LjcyIDY3LjkyLDQwLjkxICIvPgogICAgPHBvbHlnb24gaWQ9IjE0MCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2Ny45OCw0MC42NyA2Ny42Miw0MS44NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDEiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjcuNjksNDEuNjIgNjcuMjksNDIuOCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjcuMzcsNDIuNTYgNjYuOTUsNDMuNzIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTQzIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY3LjAzLDQzLjQ5IDY2LjU4LDQ0LjY0ICIvPgogICAgPHBvbHlnb24gaWQ9IjE0NCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2Ni42Nyw0NC40MSA2Ni4xOSw0NS41NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjYuMjksNDUuMzMgNjUuNzgsNDYuNDUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTQ2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY1Ljg4LDQ2LjIzIDY1LjM0LDQ3LjM0ICIvPgogICAgPHBvbHlnb24gaWQ9IjE0NyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2NS40NSw0Ny4xMiA2NC44OCw0OC4yMiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjUsNDggNjQuNCw0OS4wOSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjQuNTIsNDguODcgNjMuOSw0OS45NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNTAiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjQuMDMsNDkuNzMgNjMuMzgsNTAuNzggIi8+CiAgICA8cG9seWdvbiBpZD0iMTUxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDYzLjUxLDUwLjU3IDYyLjg0LDUxLjYxICIvPgogICAgPHBvbHlnb24gaWQ9IjE1MiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2Mi45Nyw1MS40IDYyLjI4LDUyLjQyICIvPgogICAgPHBvbHlnb24gaWQ9IjE1MyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2Mi40Miw1Mi4yMiA2MS43LDUzLjIyICIvPgogICAgPHBvbHlnb24gaWQ9IjE1NCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2MS44NCw1My4wMiA2MS4wOSw1NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNTUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjEuMjQsNTMuODEgNjAuNDcsNTQuNzcgIi8+CiAgICA8cG9seWdvbiBpZD0iMTU2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDYwLjYzLDU0LjU4IDU5LjgzLDU1LjUyICIvPgogICAgPHBvbHlnb24gaWQ9IjE1NyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA1OS45OSw1NS4zNCA1OS4xNyw1Ni4yNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNTgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNTkuMzQsNTYuMDggNTguNDksNTYuOTggIi8+CiAgICA8cG9seWdvbiBpZD0iMTU5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDU4LjY2LDU2LjggNTcuOCw1Ny42OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNjAiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNTcuOTcsNTcuNTEgNTcuMDksNTguMzcgIi8+CiAgICA8cG9seWdvbiBpZD0iMTYxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDU3LjI2LDU4LjE5IDU2LjM2LDU5LjAzICIvPgogICAgPHBvbHlnb24gaWQ9IjE2MiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA1Ni41NCw1OC44NyA1NS42MSw1OS42OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNjMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNTUuOCw1OS41MiA1NC44NSw2MC4zMSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNjQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNTUuMDQsNjAuMTUgNTQuMDcsNjAuOTIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTY1IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDU0LjI3LDYwLjc3IDUzLjI4LDYxLjUxICIvPgogICAgPHBvbHlnb24gaWQ9IjE2NiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA1My40OCw2MS4zNiA1Mi40Nyw2Mi4wOCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNjciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNTIuNjcsNjEuOTQgNTEuNjUsNjIuNjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTY4IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDUxLjg2LDYyLjUgNTAuODIsNjMuMTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTY5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDUxLjAyLDYzLjAzIDQ5Ljk3LDYzLjY3ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3MCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA1MC4xOCw2My41NSA0OS4xMSw2NC4xNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNzEiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNDkuMzIsNjQuMDQgNDguMjMsNjQuNjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTcyIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQ4LjQ1LDY0LjUxIDQ3LjM1LDY1LjA3ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3MyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA0Ny41Nyw2NC45NiA0Ni40NSw2NS41ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3NCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA0Ni42OCw2NS4zOSA0NS41NSw2NS45ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3NSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA0NS43Nyw2NS43OSA0NC42Myw2Ni4yNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNzYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNDQuODYsNjYuMTggNDMuNzEsNjYuNjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTc3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQzLjk0LDY2LjU0IDQyLjc3LDY2Ljk2ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA0Myw2Ni44OCA0MS44Myw2Ny4yNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNzkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNDIuMDYsNjcuMTkgNDAuODgsNjcuNTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTgwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQxLjEyLDY3LjQ4IDM5LjkyLDY3LjgyICIvPgogICAgPHBvbHlnb24gaWQ9IjE4MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA0MC4xNiw2Ny43NSAzOC45Niw2OC4wNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMzkuMiw2OCAzNy45OSw2OC4yNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMzguMjMsNjguMjIgMzcuMDEsNjguNDYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTg0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDM3LjI1LDY4LjQxIDM2LjAzLDY4LjYzICIvPgogICAgPHBvbHlnb24gaWQ9IjE4NSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAzNi4yOCw2OC41OCAzNS4wNSw2OC43NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMzUuMjksNjguNzMgMzQuMDYsNjguODkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTg3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDM0LjMsNjguODYgMzMuMDcsNjguOTggIi8+CiAgICA8cG9seWdvbiBpZD0iMTg4IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDMzLjMxLDY4Ljk2IDMyLjA3LDY5LjA1ICIvPgogICAgPHBvbHlnb24gaWQ9IjE4OSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAzMi4zMiw2OS4wMyAzMS4wOCw2OS4xICIvPgogICAgPHBvbHlnb24gaWQ9IjE5MCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAzMS4zMyw2OS4wOCAzMC4wOCw2OS4xMiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOTEiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMzAuMzMsNjkuMTEgMjkuMDgsNjkuMTEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTkyIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI5LjMzLDY5LjExIDI4LjA4LDY5LjA4ICIvPgogICAgPHBvbHlnb24gaWQ9IjE5MyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAyOC4zMyw2OS4wOSAyNy4wOSw2OS4wMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOTQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMjcuMzQsNjkuMDQgMjYuMDksNjguOTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTk1IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI2LjM0LDY4Ljk3IDI1LjEsNjguODUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTk2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI1LjM1LDY4Ljg3IDI0LjEsNjguNzIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTk3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI0LjM1LDY4Ljc1IDIzLjEyLDY4LjU3ICIvPgogICAgPHBvbHlnb24gaWQ9IjE5OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAyMy4zNiw2OC42MSAyMi4xMyw2OC40ICIvPgogICAgPHBvbHlnb24gaWQ9IjE5OSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAyMi4zOCw2OC40NCAyMS4xNSw2OC4yICIvPgogICAgPHBvbHlnb24gaWQ9IjIwMCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAyMS4zOSw2OC4yNSAyMC4xNyw2Ny45OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDEiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMjAuNDIsNjguMDMgMTkuMiw2Ny43MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMTkuNDQsNjcuNzkgMTguMjQsNjcuNDYgIi8+CiAgICA8cG9seWdvbiBpZD0iMjAzIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDE4LjQ4LDY3LjUzIDE3LjI4LDY3LjE3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIwNCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAxNy41Miw2Ny4yNCAxNi4zMyw2Ni44NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMTYuNTYsNjYuOTMgMTUuMzgsNjYuNTEgIi8+CiAgICA8cG9seWdvbiBpZD0iMjA2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDE1LjYyLDY2LjU5IDE0LjQ0LDY2LjE1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIwNyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAxNC42OCw2Ni4yNCAxMy41Miw2NS43NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMTMuNzUsNjUuODYgMTIuNiw2NS4zNSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMTIuODMsNjUuNDYgMTEuNjksNjQuOTIgIi8+CiAgICA8cG9seWdvbiBpZD0iMjEwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDExLjkyLDY1LjAzIDEwLjc5LDY0LjQ3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxMSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAxMS4wMiw2NC41OCA5LjkxLDY0ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxMiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAxMC4xMyw2NC4xMiA5LjAzLDYzLjUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjEzIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDkuMjUsNjMuNjMgOC4xNyw2Mi45OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMTQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggOC4zOSw2My4xMSA3LjMyLDYyLjQ1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxNSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA3LjUzLDYyLjU4IDYuNDgsNjEuODkgIi8+CiAgICA8cG9seWdvbiBpZD0iMjE2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDYuNjksNjIuMDMgNS42Niw2MS4zMSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMTciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNS44Niw2MS40NiA0Ljg1LDYwLjcyICIvPgogICAgPHBvbHlnb24gaWQ9IjIxOCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA1LjA1LDYwLjg3IDQuMDUsNjAuMSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMTkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNC4yNSw2MC4yNSAzLjI3LDU5LjQ2ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyMCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAzLjQ3LDU5LjYyIDIuNTEsNTguODEgIi8+CiAgICA8cG9seWdvbiBpZD0iMjIxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDIuNyw1OC45NyAxLjc2LDU4LjE0ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyMiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAxLjk0LDU4LjMgMS4wMiw1Ny40NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMS4yMSw1Ny42MiAwLjMxLDU2Ljc0ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyNCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAwLjQ5LDU2LjkxIC0wLjM5LDU2LjAxICIvPgogICAgPHBvbHlnb24gaWQ9IjIyNSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtMC4yMSw1Ni4xOSAtMS4wNyw1NS4yNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTAuOSw1NS40NSAtMS43Myw1NC41MSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTEuNTcsNTQuNyAtMi4zOCw1My43NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTIuMjIsNTMuOTMgLTMsNTIuOTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjI5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0yLjg1LDUzLjE1IC0zLjYxLDUyLjE1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzMCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtMy40Niw1Mi4zNSAtNC4yLDUxLjMzICIvPgogICAgPHBvbHlnb24gaWQ9IjIzMSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtNC4wNSw1MS41MyAtNC43Niw1MC41ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzMiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtNC42Miw1MC43IC01LjMxLDQ5LjY1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzMyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtNS4xNyw0OS44NiAtNS44Myw0OC43OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMzQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTUuNyw0OS4wMSAtNi4zNCw0Ny45MiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMzUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTYuMjEsNDguMTQgLTYuODIsNDcuMDQgIi8+CiAgICA8cG9seWdvbiBpZD0iMjM2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC02LjcsNDcuMjYgLTcuMjgsNDYuMTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjM3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC03LjE3LDQ2LjM3IC03LjcyLDQ1LjI1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzOCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtNy42MSw0NS40NyAtOC4xNCw0NC4zMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMzkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTguMDMsNDQuNTYgLTguNTMsNDMuNDEgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC04LjQzLDQzLjY0IC04LjkxLDQyLjQ4ICIvPgogICAgPHBvbHlnb24gaWQ9IjI0MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtOC44MSw0Mi43MSAtOS4yNiw0MS41NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTkuMTcsNDEuNzcgLTkuNTgsNDAuNTkgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQzIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC05LjUsNDAuODIgLTkuODksMzkuNjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQ0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC05LjgxLDM5Ljg3IC0xMC4xNywzOC42NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTEwLjEsMzguOTEgLTEwLjQyLDM3LjcgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQ2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMC4zNiwzNy45NCAtMTAuNjYsMzYuNzMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQ3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMC42LDM2Ljk3IC0xMC44NywzNS43NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTEwLjgxLDM1Ljk5IC0xMS4wNSwzNC43NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTExLDM1LjAxIC0xMS4yMSwzMy43OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNTAiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTExLjE3LDM0LjAyIC0xMS4zNSwzMi43OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNTEiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTExLjMxLDMzLjAzIC0xMS40NiwzMS43OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNTIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTExLjQzLDMyLjA0IC0xMS41NSwzMC44ICIvPgogICAgPHBvbHlnb24gaWQ9IjI1MyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtMTEuNTIsMzEuMDUgLTExLjYxLDI5LjggIi8+CiAgICA8cG9seWdvbiBpZD0iMjU0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMS41OSwzMC4wNSAtMTEuNjUsMjguODEgIi8+CiAgICA8cG9seWdvbiBpZD0iMjU1IiBjbGFzcz0iZmlsMTI4IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMS42NCwyOS4wNSAtMTEuNjYsMjguMDYgIi8+CiAgIDwvZz4KICA8L2c+CiA8L2c+Cjwvc3ZnPg==");
}
	.large-2qn7A4BC .semicircle-2qn7A4BC{
		width:306px;
		height:153px;
		border-top-left-radius:306px;
		border-top-right-radius:306px
}
	.large-2qn7A4BC .arrow-2qn7A4BC{
		height:145px
}
	.large-2qn7A4BC .arrowMain-2qn7A4BC{
		height:130px
}
}
.small-2qn7A4BC .sizeWrapper-2qn7A4BC{
	width:154px;
	height:77px;
	margin-top:15px
}
.small-2qn7A4BC .bottomSignals-2qn7A4BC,.small-2qn7A4BC .middleSignals-2qn7A4BC{
	margin:13px 0
}
.small-2qn7A4BC .middleSignals-2qn7A4BC{
	width:192px
}
.small-2qn7A4BC .bottomSignals-2qn7A4BC{
	width:256px
}
.small-2qn7A4BC .speedometerText-2qn7A4BC{
	font-size:9px;
	width:48px
}
.small-2qn7A4BC .circleWrapper-2qn7A4BC{
	width:154px;
	height:77px;
	background-image:url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbDpzcGFjZT0icHJlc2VydmUiIHdpZHRoPSIyMjBweCIgaGVpZ2h0PSIxMTBweCIgdmVyc2lvbj0iMS4xIiBzdHlsZT0ic2hhcGUtcmVuZGVyaW5nOmdlb21ldHJpY1ByZWNpc2lvbjsgdGV4dC1yZW5kZXJpbmc6Z2VvbWV0cmljUHJlY2lzaW9uOyBpbWFnZS1yZW5kZXJpbmc6b3B0aW1pemVRdWFsaXR5OyBmaWxsLXJ1bGU6ZXZlbm9kZDsgY2xpcC1ydWxlOmV2ZW5vZGQiCnZpZXdCb3g9IjAgMCAzOS43MyAxOS44NiIKIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIj4KIDxkZWZzPgogIDxzdHlsZSB0eXBlPSJ0ZXh0L2NzcyI+CiAgIDwhW0NEQVRBWwogICAgLmZpbDY0IHtmaWxsOiMwMEIyQzZ9CiAgICAuZmlsNjMge2ZpbGw6IzAwQjJDOH0KICAgIC5maWw2NyB7ZmlsbDojMDBCM0MwfQogICAgLmZpbDY2IHtmaWxsOiMwMEIzQzJ9CiAgICAuZmlsNjUge2ZpbGw6IzAwQjNDNH0KICAgIC5maWw3MCB7ZmlsbDojMDBCNEJCfQogICAgLmZpbDY5IHtmaWxsOiMwMEI0QkR9CiAgICAuZmlsNjgge2ZpbGw6IzAwQjRCRn0KICAgIC5maWw3MyB7ZmlsbDojMDBCNUI2fQogICAgLmZpbDcyIHtmaWxsOiMwMEI1Qjh9CiAgICAuZmlsNzEge2ZpbGw6IzAwQjVCOX0KICAgIC5maWw3NiB7ZmlsbDojMDBCNkIxfQogICAgLmZpbDc1IHtmaWxsOiMwMEI2QjJ9CiAgICAuZmlsNzQge2ZpbGw6IzAwQjZCNH0KICAgIC5maWw3OSB7ZmlsbDojMDBCN0FCfQogICAgLmZpbDc4IHtmaWxsOiMwMEI3QUR9CiAgICAuZmlsNzcge2ZpbGw6IzAwQjdBRn0KICAgIC5maWw4MiB7ZmlsbDojMDBCOEE2fQogICAgLmZpbDgxIHtmaWxsOiMwMEI4QTh9CiAgICAuZmlsODAge2ZpbGw6IzAwQjhBOX0KICAgIC5maWw4NSB7ZmlsbDojMDBCOUExfQogICAgLmZpbDg0IHtmaWxsOiMwMEI5QTJ9CiAgICAuZmlsODMge2ZpbGw6IzAwQjlBNH0KICAgIC5maWw4OCB7ZmlsbDojMDBCQTlCfQogICAgLmZpbDg3IHtmaWxsOiMwMEJBOUR9CiAgICAuZmlsODYge2ZpbGw6IzAwQkE5Rn0KICAgIC5maWw5MSB7ZmlsbDojMDBCQjk2fQogICAgLmZpbDkwIHtmaWxsOiMwMEJCOTh9CiAgICAuZmlsODkge2ZpbGw6IzAwQkI5OX0KICAgIC5maWw5NCB7ZmlsbDojMDBCQzkxfQogICAgLmZpbDkzIHtmaWxsOiMwMEJDOTJ9CiAgICAuZmlsOTIge2ZpbGw6IzAwQkM5NH0KICAgIC5maWw5NyB7ZmlsbDojMDBCRDhCfQogICAgLmZpbDk2IHtmaWxsOiMwMEJEOER9CiAgICAuZmlsOTUge2ZpbGw6IzAwQkQ4Rn0KICAgIC5maWwxMDAge2ZpbGw6IzAwQkU4Nn0KICAgIC5maWw5OSB7ZmlsbDojMDBCRTg4fQogICAgLmZpbDk4IHtmaWxsOiMwMEJFOEF9CiAgICAuZmlsMTAzIHtmaWxsOiMwMEJGODF9CiAgICAuZmlsMTAyIHtmaWxsOiMwMEJGODJ9CiAgICAuZmlsMTAxIHtmaWxsOiMwMEJGODR9CiAgICAuZmlsMTA2IHtmaWxsOiMwMEMwN0J9CiAgICAuZmlsMTA1IHtmaWxsOiMwMEMwN0R9CiAgICAuZmlsMTA0IHtmaWxsOiMwMEMwN0Z9CiAgICAuZmlsMTA5IHtmaWxsOiMwMEMxNzZ9CiAgICAuZmlsMTA4IHtmaWxsOiMwMEMxNzh9CiAgICAuZmlsMTA3IHtmaWxsOiMwMEMxN0F9CiAgICAuZmlsMTEyIHtmaWxsOiMwMEMyNzF9CiAgICAuZmlsMTExIHtmaWxsOiMwMEMyNzJ9CiAgICAuZmlsMTEwIHtmaWxsOiMwMEMyNzR9CiAgICAuZmlsMTE1IHtmaWxsOiMwMEMzNkJ9CiAgICAuZmlsMTE0IHtmaWxsOiMwMEMzNkR9CiAgICAuZmlsMTEzIHtmaWxsOiMwMEMzNkZ9CiAgICAuZmlsMTE4IHtmaWxsOiMwMEM0NjZ9CiAgICAuZmlsMTE3IHtmaWxsOiMwMEM0Njh9CiAgICAuZmlsMTE2IHtmaWxsOiMwMEM0NkF9CiAgICAuZmlsMTIxIHtmaWxsOiMwMEM1NjF9CiAgICAuZmlsMTIwIHtmaWxsOiMwMEM1NjN9CiAgICAuZmlsMTE5IHtmaWxsOiMwMEM1NjR9CiAgICAuZmlsMTI0IHtmaWxsOiMwMEM2NUJ9CiAgICAuZmlsMTIzIHtmaWxsOiMwMEM2NUR9CiAgICAuZmlsMTIyIHtmaWxsOiMwMEM2NUZ9CiAgICAuZmlsMTI3IHtmaWxsOiMwMEM3NTd9CiAgICAuZmlsMTI2IHtmaWxsOiMwMEM3NTh9CiAgICAuZmlsMTI1IHtmaWxsOiMwMEM3NUF9CiAgICAuZmlsNjIge2ZpbGw6IzAzQjBDNn0KICAgIC5maWw2MSB7ZmlsbDojMDdBREM0fQogICAgLmZpbDYwIHtmaWxsOiMwQkFBQzJ9CiAgICAuZmlsNTkge2ZpbGw6IzBGQThDMH0KICAgIC5maWw1OCB7ZmlsbDojMTNBNUJFfQogICAgLmZpbDU3IHtmaWxsOiMxN0EyQkN9CiAgICAuZmlsNTYge2ZpbGw6IzFCOUZCQX0KICAgIC5maWw1NSB7ZmlsbDojMUY5Q0I3fQogICAgLmZpbDU0IHtmaWxsOiMyMzlBQjV9CiAgICAuZmlsNTMge2ZpbGw6IzI3OTdCM30KICAgIC5maWw1MiB7ZmlsbDojMkI5NEIxfQogICAgLmZpbDUxIHtmaWxsOiMyRjkxQUZ9CiAgICAuZmlsNTAge2ZpbGw6IzMzOEVBRH0KICAgIC5maWw0OSB7ZmlsbDojMzc4Q0FCfQogICAgLmZpbDQ4IHtmaWxsOiMzQjg5QTl9CiAgICAuZmlsNDcge2ZpbGw6IzNGODZBNn0KICAgIC5maWw0NiB7ZmlsbDojNDM4M0E0fQogICAgLmZpbDQ1IHtmaWxsOiM0NzgwQTJ9CiAgICAuZmlsNDQge2ZpbGw6IzRCN0VBMH0KICAgIC5maWw0MyB7ZmlsbDojNEY3QjlFfQogICAgLmZpbDQyIHtmaWxsOiM1Mzc4OUN9CiAgICAuZmlsNDEge2ZpbGw6IzU3NzU5QX0KICAgIC5maWw0MCB7ZmlsbDojNUI3Mjk3fQogICAgLmZpbDM5IHtmaWxsOiM1RjcwOTV9CiAgICAuZmlsMzgge2ZpbGw6IzYzNkQ5M30KICAgIC5maWwzNyB7ZmlsbDojNjc2QTkxfQogICAgLmZpbDM2IHtmaWxsOiM2QjY3OEZ9CiAgICAuZmlsMzUge2ZpbGw6IzZGNjU4RH0KICAgIC5maWwzNCB7ZmlsbDojNzM2MjhCfQogICAgLmZpbDMzIHtmaWxsOiM3NzVGODl9CiAgICAuZmlsMzIge2ZpbGw6IzdCNUM4Nn0KICAgIC5maWwzMSB7ZmlsbDojN0Y1OTg0fQogICAgLmZpbDMwIHtmaWxsOiM4MzU3ODJ9CiAgICAuZmlsMjkge2ZpbGw6Izg3NTQ4MH0KICAgIC5maWwyOCB7ZmlsbDojOEI1MTdFfQogICAgLmZpbDI3IHtmaWxsOiM4RjRFN0N9CiAgICAuZmlsMjYge2ZpbGw6IzkzNEI3QX0KICAgIC5maWwyNSB7ZmlsbDojOTc0OTc3fQogICAgLmZpbDI0IHtmaWxsOiM5QjQ2NzV9CiAgICAuZmlsMjMge2ZpbGw6IzlGNDM3M30KICAgIC5maWwyMiB7ZmlsbDojQTM0MDcxfQogICAgLmZpbDIxIHtmaWxsOiNBNzNENkZ9CiAgICAuZmlsMjAge2ZpbGw6I0FCM0I2RH0KICAgIC5maWwxOSB7ZmlsbDojQUYzODZCfQogICAgLmZpbDE4IHtmaWxsOiNCMzM1Njl9CiAgICAuZmlsMTcge2ZpbGw6I0I3MzI2Nn0KICAgIC5maWwxNiB7ZmlsbDojQkIyRjY0fQogICAgLmZpbDE1IHtmaWxsOiNCRjJENjJ9CiAgICAuZmlsMTQge2ZpbGw6I0MzMkE2MH0KICAgIC5maWwxMyB7ZmlsbDojQzcyNzVFfQogICAgLmZpbDEyIHtmaWxsOiNDQjI0NUN9CiAgICAuZmlsMTEge2ZpbGw6I0NGMjI1QX0KICAgIC5maWwxMCB7ZmlsbDojRDMxRjU3fQogICAgLmZpbDkge2ZpbGw6I0Q3MUM1NX0KICAgIC5maWw4IHtmaWxsOiNEQjE5NTN9CiAgICAuZmlsNyB7ZmlsbDojREYxNjUxfQogICAgLmZpbDYge2ZpbGw6I0UzMTQ0Rn0KICAgIC5maWw1IHtmaWxsOiNFNzExNER9CiAgICAuZmlsNCB7ZmlsbDojRUIwRTRCfQogICAgLmZpbDMge2ZpbGw6I0VGMEI0OX0KICAgIC5maWwyIHtmaWxsOiNGMzA4NDZ9CiAgICAuZmlsMSB7ZmlsbDojRjcwNjQ0fQogICAgLmZpbDAge2ZpbGw6I0ZCMDM0Mn0KICAgIC5maWwxMjgge2ZpbGw6I0ZGMDA0MH0KICAgXV0+CiAgPC9zdHlsZT4KICAgIDxjbGlwUGF0aCBpZD0iaWQwIj4KICAgICA8cGF0aCBkPSJNMy41IDguNmMwLjA1LC0wLjA3IDAuMTIsLTAuMTEgMC4yLC0wLjExIDAuMDYsMCAwLjExLDAuMDIgMC4xNSwwLjA1IDAuMTEsMC4wOCAwLjE0LDAuMjQgMC4wNiwwLjM1IC0yLjE3LDMuMTUgLTMuMzYsNi44OSAtMy40MSwxMC43MiAwLDAuMTQgLTAuMTEsMC4yNSAtMC4yNSwwLjI1IC0wLjE0LDAgLTAuMjUsLTAuMTEgLTAuMjUsLTAuMjUgMCwwIDAsMCAwLDAgMC4wNSwtNC4wOCAxLjM0LC03Ljg3IDMuNSwtMTEuMDFsMCAwem0zMi4zOCAtMC4wNmMtMC4wNywwLjA1IC0wLjExLDAuMTMgLTAuMTEsMC4yMSAwLDAuMDUgMC4wMiwwLjEgMC4wNSwwLjE0IDIuMTcsMy4xNSAzLjM2LDYuODkgMy40LDEwLjcyIDAsMC4xNCAwLjEyLDAuMjUgMC4yNiwwLjI1IDAuMTQsMCAwLjI1LC0wLjExIDAuMjUsLTAuMjUgMCwwIDAsMCAwLDAgLTAuMDQsLTMuOTMgLTEuMjcsLTcuNzcgLTMuNSwtMTEuMDEgLTAuMDUsLTAuMDcgLTAuMTIsLTAuMTEgLTAuMjEsLTAuMTEgLTAuMDUsMCAtMC4xLDAuMDIgLTAuMTQsMC4wNWwwIDB6bS05LjQ5IC02LjkxYy0wLjExLC0wLjA0IC0wLjE3LC0wLjEzIC0wLjE3LC0wLjI0IDAsLTAuMDMgMCwtMC4wNSAwLjAxLC0wLjA4IDAuMDMsLTAuMSAwLjEzLC0wLjE3IDAuMjQsLTAuMTcgMC4wMiwwIDAuMDUsMCAwLjA4LDAuMDEgMy42LDEuMjkgNi43NiwzLjYgOS4wOCw2LjYzIDAuMDksMC4xMSAwLjA2LDAuMjcgLTAuMDUsMC4zNSAtMC4wNCwwLjA0IC0wLjEsMC4wNSAtMC4xNSwwLjA1IC0wLjA4LDAgLTAuMTUsLTAuMDMgLTAuMiwtMC4xIC0yLjI3LC0yLjk1IC01LjM0LC01LjE5IC04Ljg0LC02LjQ1bDAgMHptLTEyLjQyIC0wLjQ4YzAuMDQsMC4xMSAwLjE0LDAuMTggMC4yNSwwLjE4IDAuMDIsMCAwLjA1LC0wLjAxIDAuMDcsLTAuMDEgMS44LC0wLjU0IDMuNjcsLTAuODIgNS41NiwtMC44MiAwLDAgMC4wMSwwIDAuMDEsMCAxLjk0LDAgMy44MSwwLjI5IDUuNTgsMC44MiAwLjAyLDAgMC4wNSwwLjAxIDAuMDcsMC4wMSAwLjExLDAgMC4yMSwtMC4wNyAwLjI0LC0wLjE4IDAuMDEsLTAuMDIgMC4wMSwtMC4wNSAwLjAxLC0wLjA3IDAsLTAuMTEgLTAuMDcsLTAuMjEgLTAuMTcsLTAuMjQgLTEuODUsLTAuNTYgLTMuNzgsLTAuODQgLTUuNzEsLTAuODQgMCwwIC0wLjAxLDAgLTAuMDIsMCAtMS45OSwwIC0zLjkxLDAuMjkgLTUuNzIsMC44NCAtMC4xMSwwLjAzIC0wLjE4LDAuMTMgLTAuMTgsMC4yNCAwLDAuMDIgMC4wMSwwLjA1IDAuMDIsMC4wN2wtMC4wMSAwem0tMC40NyAwLjE2YzAuMDEsMC4wMyAwLjAxLDAuMDUgMC4wMSwwLjA4IDAsMC4xMSAtMC4wNywwLjIgLTAuMTcsMC4yNCAtMy41LDEuMjUgLTYuNTgsMy41IC04Ljg0LDYuNDUgLTAuMDUsMC4wNyAtMC4xMiwwLjEgLTAuMiwwLjEgLTAuMDYsMCAtMC4xMSwtMC4wMSAtMC4xNSwtMC4wNSAtMC4wNywtMC4wNCAtMC4xLC0wLjEyIC0wLjEsLTAuMiAwLC0wLjA1IDAuMDEsLTAuMSAwLjA1LC0wLjE1IDIuMzIsLTMuMDMgNS40OCwtNS4zNCA5LjA4LC02LjYzIDAuMTMsLTAuMDQgMC4yNywwLjAzIDAuMzIsMC4xNmwwIDB6Ii8+CiAgICA8L2NsaXBQYXRoPgogPC9kZWZzPgogPGcgaWQ9IjEiPgogIDxnPgogICA8ZyBzdHlsZT0iY2xpcC1wYXRoOnVybCgjaWQwKSI+CiAgICA8cG9seWdvbiBjbGFzcz0iZmlsMCIgcG9pbnRzPSIyMC4xOCwxOS44MyAtOC4xMiwxOS43MSAtOC4xMSwxOC42NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxIiBjbGFzcz0iZmlsMSIgcG9pbnRzPSIyMC4xOCwxOS44MyAtOC4xMiwxOC44NCAtOC4wOSwxNy45NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyIiBjbGFzcz0iZmlsMiIgcG9pbnRzPSIyMC4xOCwxOS44MyAtOC4xLDE4LjE1IC04LjA1LDE3LjI4ICIvPgogICAgPHBvbHlnb24gaWQ9IjMiIGNsYXNzPSJmaWwzIiBwb2ludHM9IjIwLjE4LDE5LjgzIC04LjA2LDE3LjQ1IC03Ljk5LDE2LjU5ICIvPgogICAgPHBvbHlnb24gaWQ9IjQiIGNsYXNzPSJmaWw0IiBwb2ludHM9IjIwLjE4LDE5LjgzIC04LjAxLDE2Ljc2IC03LjkyLDE1LjkgIi8+CiAgICA8cG9seWdvbiBpZD0iNSIgY2xhc3M9ImZpbDUiIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuOTMsMTYuMDcgLTcuODMsMTUuMjEgIi8+CiAgICA8cG9seWdvbiBpZD0iNiIgY2xhc3M9ImZpbDYiIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuODUsMTUuMzkgLTcuNzIsMTQuNTMgIi8+CiAgICA8cG9seWdvbiBpZD0iNyIgY2xhc3M9ImZpbDciIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuNzQsMTQuNyAtNy41OSwxMy44NSAiLz4KICAgIDxwb2x5Z29uIGlkPSI4IiBjbGFzcz0iZmlsOCIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNy42MiwxNC4wMiAtNy40NSwxMy4xNyAiLz4KICAgIDxwb2x5Z29uIGlkPSI5IiBjbGFzcz0iZmlsOSIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNy40OCwxMy4zNCAtNy4yOSwxMi41ICIvPgogICAgPHBvbHlnb24gaWQ9IjEwIiBjbGFzcz0iZmlsMTAiIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuMzMsMTIuNjcgLTcuMTEsMTEuODMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTEiIGNsYXNzPSJmaWwxMSIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNy4xNiwxMiAtNi45MiwxMS4xNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMiIgY2xhc3M9ImZpbDEyIiBwb2ludHM9IjIwLjE4LDE5LjgzIC02Ljk3LDExLjMzIC02LjcxLDEwLjUxICIvPgogICAgPHBvbHlnb24gaWQ9IjEzIiBjbGFzcz0iZmlsMTMiIHBvaW50cz0iMjAuMTgsMTkuODMgLTYuNzcsMTAuNjcgLTYuNDksOS44NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNCIgY2xhc3M9ImZpbDE0IiBwb2ludHM9IjIwLjE4LDE5LjgzIC02LjU0LDEwLjAyIC02LjI1LDkuMjEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTUiIGNsYXNzPSJmaWwxNSIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNi4zMSw5LjM3IC01Ljk5LDguNTcgIi8+CiAgICA8cG9seWdvbiBpZD0iMTYiIGNsYXNzPSJmaWwxNiIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNi4wNiw4LjczIC01LjcyLDcuOTQgIi8+CiAgICA8cG9seWdvbiBpZD0iMTciIGNsYXNzPSJmaWwxNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNS43OSw4LjA5IC01LjQzLDcuMzEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTgiIGNsYXNzPSJmaWwxOCIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNS41LDcuNDcgLTUuMTMsNi42OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOSIgY2xhc3M9ImZpbDE5IiBwb2ludHM9IjIwLjE4LDE5LjgzIC01LjIsNi44NSAtNC44MSw2LjA4ICIvPgogICAgPHBvbHlnb24gaWQ9IjIwIiBjbGFzcz0iZmlsMjAiIHBvaW50cz0iMjAuMTgsMTkuODMgLTQuODksNi4yMyAtNC40OCw1LjQ4ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxIiBjbGFzcz0iZmlsMjEiIHBvaW50cz0iMjAuMTgsMTkuODMgLTQuNTYsNS42MyAtNC4xMyw0Ljg4ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyIiBjbGFzcz0iZmlsMjIiIHBvaW50cz0iMjAuMTgsMTkuODMgLTQuMjIsNS4wMyAtMy43Nyw0LjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjMiIGNsYXNzPSJmaWwyMyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMy44Niw0LjQ0IC0zLjM5LDMuNzIgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQiIGNsYXNzPSJmaWwyNCIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMy40OCwzLjg3IC0zLDMuMTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMjUiIGNsYXNzPSJmaWwyNSIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMy4wOSwzLjMgLTIuNTksMi42ICIvPgogICAgPHBvbHlnb24gaWQ9IjI2IiBjbGFzcz0iZmlsMjYiIHBvaW50cz0iMjAuMTgsMTkuODMgLTIuNjksMi43NCAtMi4xNywyLjA1ICIvPgogICAgPHBvbHlnb24gaWQ9IjI3IiBjbGFzcz0iZmlsMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTIuMjgsMi4xOSAtMS43NCwxLjUyICIvPgogICAgPHBvbHlnb24gaWQ9IjI4IiBjbGFzcz0iZmlsMjgiIHBvaW50cz0iMjAuMTgsMTkuODMgLTEuODUsMS42NSAtMS4yOSwwLjk5ICIvPgogICAgPHBvbHlnb24gaWQ9IjI5IiBjbGFzcz0iZmlsMjkiIHBvaW50cz0iMjAuMTgsMTkuODMgLTEuNCwxLjEzIC0wLjgzLDAuNDggIi8+CiAgICA8cG9seWdvbiBpZD0iMzAiIGNsYXNzPSJmaWwzMCIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMC45NSwwLjYxIC0wLjM2LC0wLjAyICIvPgogICAgPHBvbHlnb24gaWQ9IjMxIiBjbGFzcz0iZmlsMzEiIHBvaW50cz0iMjAuMTgsMTkuODMgLTAuNDgsMC4xMSAwLjEyLC0wLjUxICIvPgogICAgPHBvbHlnb24gaWQ9IjMyIiBjbGFzcz0iZmlsMzIiIHBvaW50cz0iMjAuMTgsMTkuODMgMCwtMC4zOSAwLjYyLC0wLjk4ICIvPgogICAgPHBvbHlnb24gaWQ9IjMzIiBjbGFzcz0iZmlsMzMiIHBvaW50cz0iMjAuMTgsMTkuODMgMC40OSwtMC44NiAxLjEyLC0xLjQ1ICIvPgogICAgPHBvbHlnb24gaWQ9IjM0IiBjbGFzcz0iZmlsMzQiIHBvaW50cz0iMjAuMTgsMTkuODMgMSwtMS4zMyAxLjY0LC0xLjkgIi8+CiAgICA8cG9seWdvbiBpZD0iMzUiIGNsYXNzPSJmaWwzNSIgcG9pbnRzPSIyMC4xOCwxOS44MyAxLjUxLC0xLjc5IDIuMTcsLTIuMzQgIi8+CiAgICA8cG9seWdvbiBpZD0iMzYiIGNsYXNzPSJmaWwzNiIgcG9pbnRzPSIyMC4xOCwxOS44MyAyLjA0LC0yLjIzIDIuNzIsLTIuNzYgIi8+CiAgICA8cG9seWdvbiBpZD0iMzciIGNsYXNzPSJmaWwzNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyLjU4LC0yLjY2IDMuMjcsLTMuMTcgIi8+CiAgICA8cG9seWdvbiBpZD0iMzgiIGNsYXNzPSJmaWwzOCIgcG9pbnRzPSIyMC4xOCwxOS44MyAzLjEzLC0zLjA3IDMuODMsLTMuNTcgIi8+CiAgICA8cG9seWdvbiBpZD0iMzkiIGNsYXNzPSJmaWwzOSIgcG9pbnRzPSIyMC4xOCwxOS44MyAzLjY5LC0zLjQ3IDQuNCwtMy45NiAiLz4KICAgIDxwb2x5Z29uIGlkPSI0MCIgY2xhc3M9ImZpbDQwIiBwb2ludHM9IjIwLjE4LDE5LjgzIDQuMjYsLTMuODYgNC45OCwtNC4zMiAiLz4KICAgIDxwb2x5Z29uIGlkPSI0MSIgY2xhc3M9ImZpbDQxIiBwb2ludHM9IjIwLjE4LDE5LjgzIDQuODQsLTQuMjMgNS41NywtNC42OCAiLz4KICAgIDxwb2x5Z29uIGlkPSI0MiIgY2xhc3M9ImZpbDQyIiBwb2ludHM9IjIwLjE4LDE5LjgzIDUuNDMsLTQuNTkgNi4xNywtNS4wMiAiLz4KICAgIDxwb2x5Z29uIGlkPSI0MyIgY2xhc3M9ImZpbDQzIiBwb2ludHM9IjIwLjE4LDE5LjgzIDYuMDIsLTQuOTMgNi43OCwtNS4zNCAiLz4KICAgIDxwb2x5Z29uIGlkPSI0NCIgY2xhc3M9ImZpbDQ0IiBwb2ludHM9IjIwLjE4LDE5LjgzIDYuNjMsLTUuMjYgNy40LC01LjY1ICIvPgogICAgPHBvbHlnb24gaWQ9IjQ1IiBjbGFzcz0iZmlsNDUiIHBvaW50cz0iMjAuMTgsMTkuODMgNy4yNCwtNS41OCA4LjAyLC01Ljk1ICIvPgogICAgPHBvbHlnb24gaWQ9IjQ2IiBjbGFzcz0iZmlsNDYiIHBvaW50cz0iMjAuMTgsMTkuODMgNy44NiwtNS44NyA4LjY1LC02LjIzICIvPgogICAgPHBvbHlnb24gaWQ9IjQ3IiBjbGFzcz0iZmlsNDciIHBvaW50cz0iMjAuMTgsMTkuODMgOC40OSwtNi4xNiA5LjI5LC02LjQ5ICIvPgogICAgPHBvbHlnb24gaWQ9IjQ4IiBjbGFzcz0iZmlsNDgiIHBvaW50cz0iMjAuMTgsMTkuODMgOS4xMywtNi40MiA5LjkzLC02Ljc0ICIvPgogICAgPHBvbHlnb24gaWQ9IjQ5IiBjbGFzcz0iZmlsNDkiIHBvaW50cz0iMjAuMTgsMTkuODMgOS43NywtNi42NyAxMC41OCwtNi45NyAiLz4KICAgIDxwb2x5Z29uIGlkPSI1MCIgY2xhc3M9ImZpbDUwIiBwb2ludHM9IjIwLjE4LDE5LjgzIDEwLjQyLC02LjkxIDExLjI0LC03LjE4ICIvPgogICAgPHBvbHlnb24gaWQ9IjUxIiBjbGFzcz0iZmlsNTEiIHBvaW50cz0iMjAuMTgsMTkuODMgMTEuMDgsLTcuMTMgMTEuOSwtNy4zOCAiLz4KICAgIDxwb2x5Z29uIGlkPSI1MiIgY2xhc3M9ImZpbDUyIiBwb2ludHM9IjIwLjE4LDE5LjgzIDExLjc0LC03LjMzIDEyLjU3LC03LjU2ICIvPgogICAgPHBvbHlnb24gaWQ9IjUzIiBjbGFzcz0iZmlsNTMiIHBvaW50cz0iMjAuMTgsMTkuODMgMTIuNCwtNy41MiAxMy4yNCwtNy43MyAiLz4KICAgIDxwb2x5Z29uIGlkPSI1NCIgY2xhc3M9ImZpbDU0IiBwb2ludHM9IjIwLjE4LDE5LjgzIDEzLjA3LC03LjY5IDEzLjkxLC03Ljg4ICIvPgogICAgPHBvbHlnb24gaWQ9IjU1IiBjbGFzcz0iZmlsNTUiIHBvaW50cz0iMjAuMTgsMTkuODMgMTMuNzUsLTcuODQgMTQuNTksLTguMDEgIi8+CiAgICA8cG9seWdvbiBpZD0iNTYiIGNsYXNzPSJmaWw1NiIgcG9pbnRzPSIyMC4xOCwxOS44MyAxNC40MiwtNy45OCAxNS4yOCwtOC4xMyAiLz4KICAgIDxwb2x5Z29uIGlkPSI1NyIgY2xhc3M9ImZpbDU3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDE1LjExLC04LjEgMTUuOTYsLTguMjMgIi8+CiAgICA8cG9seWdvbiBpZD0iNTgiIGNsYXNzPSJmaWw1OCIgcG9pbnRzPSIyMC4xOCwxOS44MyAxNS43OSwtOC4yIDE2LjY1LC04LjMxICIvPgogICAgPHBvbHlnb24gaWQ9IjU5IiBjbGFzcz0iZmlsNTkiIHBvaW50cz0iMjAuMTgsMTkuODMgMTYuNDgsLTguMjkgMTcuMzQsLTguMzcgIi8+CiAgICA8cG9seWdvbiBpZD0iNjAiIGNsYXNzPSJmaWw2MCIgcG9pbnRzPSIyMC4xOCwxOS44MyAxNy4xNywtOC4zNiAxOC4wMywtOC40MiAiLz4KICAgIDxwb2x5Z29uIGlkPSI2MSIgY2xhc3M9ImZpbDYxIiBwb2ludHM9IjIwLjE4LDE5LjgzIDE3Ljg2LC04LjQxIDE4LjczLC04LjQ1ICIvPgogICAgPHBvbHlnb24gaWQ9IjYyIiBjbGFzcz0iZmlsNjIiIHBvaW50cz0iMjAuMTgsMTkuODMgMTguNTUsLTguNDUgMTkuNDIsLTguNDcgIi8+CiAgICA8cG9seWdvbiBpZD0iNjMiIGNsYXNzPSJmaWw2MyIgcG9pbnRzPSIyMC4xOCwxOS44MyAxOS4yNSwtOC40NiAyMC4xMSwtOC40NyAiLz4KICAgIDxwb2x5Z29uIGlkPSI2NCIgY2xhc3M9ImZpbDY0IiBwb2ludHM9IjIwLjE4LDE5LjgzIDE5Ljk0LC04LjQ2IDIwLjgxLC04LjQ1ICIvPgogICAgPHBvbHlnb24gaWQ9IjY1IiBjbGFzcz0iZmlsNjUiIHBvaW50cz0iMjAuMTgsMTkuODMgMjAuNjQsLTguNDUgMjEuNSwtOC40MSAiLz4KICAgIDxwb2x5Z29uIGlkPSI2NiIgY2xhc3M9ImZpbDY2IiBwb2ludHM9IjIwLjE4LDE5LjgzIDIxLjMzLC04LjQyIDIyLjIsLTguMzUgIi8+CiAgICA8cG9seWdvbiBpZD0iNjciIGNsYXNzPSJmaWw2NyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyMi4wMiwtOC4zNyAyMi44OSwtOC4yOCAiLz4KICAgIDxwb2x5Z29uIGlkPSI2OCIgY2xhc3M9ImZpbDY4IiBwb2ludHM9IjIwLjE4LDE5LjgzIDIyLjcyLC04LjMgMjMuNTgsLTguMiAiLz4KICAgIDxwb2x5Z29uIGlkPSI2OSIgY2xhc3M9ImZpbDY5IiBwb2ludHM9IjIwLjE4LDE5LjgzIDIzLjQxLC04LjIyIDI0LjI3LC04LjA5ICIvPgogICAgPHBvbHlnb24gaWQ9IjcwIiBjbGFzcz0iZmlsNzAiIHBvaW50cz0iMjAuMTgsMTkuODMgMjQuMSwtOC4xMiAyNC45NSwtNy45NyAiLz4KICAgIDxwb2x5Z29uIGlkPSI3MSIgY2xhc3M9ImZpbDcxIiBwb2ludHM9IjIwLjE4LDE5LjgzIDI0Ljc4LC04IDI1LjY0LC03LjgzICIvPgogICAgPHBvbHlnb24gaWQ9IjcyIiBjbGFzcz0iZmlsNzIiIHBvaW50cz0iMjAuMTgsMTkuODMgMjUuNDcsLTcuODYgMjYuMzIsLTcuNjggIi8+CiAgICA8cG9seWdvbiBpZD0iNzMiIGNsYXNzPSJmaWw3MyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyNi4xNSwtNy43MSAyNi45OSwtNy41ICIvPgogICAgPHBvbHlnb24gaWQ9Ijc0IiBjbGFzcz0iZmlsNzQiIHBvaW50cz0iMjAuMTgsMTkuODMgMjYuODIsLTcuNTUgMjcuNjcsLTcuMzIgIi8+CiAgICA8cG9seWdvbiBpZD0iNzUiIGNsYXNzPSJmaWw3NSIgcG9pbnRzPSIyMC4xOCwxOS44MyAyNy41LC03LjM2IDI4LjMzLC03LjExICIvPgogICAgPHBvbHlnb24gaWQ9Ijc2IiBjbGFzcz0iZmlsNzYiIHBvaW50cz0iMjAuMTgsMTkuODMgMjguMTcsLTcuMTYgMjksLTYuODkgIi8+CiAgICA8cG9seWdvbiBpZD0iNzciIGNsYXNzPSJmaWw3NyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyOC44MywtNi45NSAyOS42NSwtNi42NSAiLz4KICAgIDxwb2x5Z29uIGlkPSI3OCIgY2xhc3M9ImZpbDc4IiBwb2ludHM9IjIwLjE4LDE5LjgzIDI5LjQ5LC02LjcxIDMwLjMsLTYuNCAiLz4KICAgIDxwb2x5Z29uIGlkPSI3OSIgY2xhc3M9ImZpbDc5IiBwb2ludHM9IjIwLjE4LDE5LjgzIDMwLjE0LC02LjQ2IDMwLjk1LC02LjEzICIvPgogICAgPHBvbHlnb24gaWQ9IjgwIiBjbGFzcz0iZmlsODAiIHBvaW50cz0iMjAuMTgsMTkuODMgMzAuNzksLTYuMiAzMS41OSwtNS44NSAiLz4KICAgIDxwb2x5Z29uIGlkPSI4MSIgY2xhc3M9ImZpbDgxIiBwb2ludHM9IjIwLjE4LDE5LjgzIDMxLjQzLC01LjkyIDMyLjIyLC01LjU1ICIvPgogICAgPHBvbHlnb24gaWQ9IjgyIiBjbGFzcz0iZmlsODIiIHBvaW50cz0iMjAuMTgsMTkuODMgMzIuMDYsLTUuNjIgMzIuODUsLTUuMjQgIi8+CiAgICA8cG9seWdvbiBpZD0iODMiIGNsYXNzPSJmaWw4MyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzMi42OSwtNS4zMSAzMy40NiwtNC45MSAiLz4KICAgIDxwb2x5Z29uIGlkPSI4NCIgY2xhc3M9ImZpbDg0IiBwb2ludHM9IjIwLjE4LDE5LjgzIDMzLjMxLC00Ljk5IDM0LjA3LC00LjU2ICIvPgogICAgPHBvbHlnb24gaWQ9Ijg1IiBjbGFzcz0iZmlsODUiIHBvaW50cz0iMjAuMTgsMTkuODMgMzMuOTIsLTQuNjUgMzQuNjcsLTQuMiAiLz4KICAgIDxwb2x5Z29uIGlkPSI4NiIgY2xhc3M9ImZpbDg2IiBwb2ludHM9IjIwLjE4LDE5LjgzIDM0LjUyLC00LjI5IDM1LjI3LC0zLjgzICIvPgogICAgPHBvbHlnb24gaWQ9Ijg3IiBjbGFzcz0iZmlsODciIHBvaW50cz0iMjAuMTgsMTkuODMgMzUuMTIsLTMuOTIgMzUuODUsLTMuNDQgIi8+CiAgICA8cG9seWdvbiBpZD0iODgiIGNsYXNzPSJmaWw4OCIgcG9pbnRzPSIyMC4xOCwxOS44MyAzNS43LC0zLjU0IDM2LjQyLC0zLjA0ICIvPgogICAgPHBvbHlnb24gaWQ9Ijg5IiBjbGFzcz0iZmlsODkiIHBvaW50cz0iMjAuMTgsMTkuODMgMzYuMjgsLTMuMTQgMzYuOTksLTIuNjIgIi8+CiAgICA8cG9seWdvbiBpZD0iOTAiIGNsYXNzPSJmaWw5MCIgcG9pbnRzPSIyMC4xOCwxOS44MyAzNi44NSwtMi43MiAzNy41NCwtMi4xOSAiLz4KICAgIDxwb2x5Z29uIGlkPSI5MSIgY2xhc3M9ImZpbDkxIiBwb2ludHM9IjIwLjE4LDE5LjgzIDM3LjQsLTIuMyAzOC4wOCwtMS43NSAiLz4KICAgIDxwb2x5Z29uIGlkPSI5MiIgY2xhc3M9ImZpbDkyIiBwb2ludHM9IjIwLjE4LDE5LjgzIDM3Ljk1LC0xLjg2IDM4LjYyLC0xLjI5ICIvPgogICAgPHBvbHlnb24gaWQ9IjkzIiBjbGFzcz0iZmlsOTMiIHBvaW50cz0iMjAuMTgsMTkuODMgMzguNDgsLTEuNDEgMzkuMTQsLTAuODIgIi8+CiAgICA8cG9seWdvbiBpZD0iOTQiIGNsYXNzPSJmaWw5NCIgcG9pbnRzPSIyMC4xOCwxOS44MyAzOS4wMSwtMC45NCAzOS42NSwtMC4zNCAiLz4KICAgIDxwb2x5Z29uIGlkPSI5NSIgY2xhc3M9ImZpbDk1IiBwb2ludHM9IjIwLjE4LDE5LjgzIDM5LjUyLC0wLjQ2IDQwLjE1LDAuMTUgIi8+CiAgICA8cG9seWdvbiBpZD0iOTYiIGNsYXNzPSJmaWw5NiIgcG9pbnRzPSIyMC4xOCwxOS44MyA0MC4wMiwwLjAzIDQwLjYzLDAuNjUgIi8+CiAgICA8cG9seWdvbiBpZD0iOTciIGNsYXNzPSJmaWw5NyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0MC41MSwwLjUzIDQxLjExLDEuMTcgIi8+CiAgICA8cG9seWdvbiBpZD0iOTgiIGNsYXNzPSJmaWw5OCIgcG9pbnRzPSIyMC4xOCwxOS44MyA0MC45OSwxLjA0IDQxLjU3LDEuNyAiLz4KICAgIDxwb2x5Z29uIGlkPSI5OSIgY2xhc3M9ImZpbDk5IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQxLjQ1LDEuNTcgNDIuMDIsMi4yNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDAiIGNsYXNzPSJmaWwxMDAiIHBvaW50cz0iMjAuMTgsMTkuODMgNDEuOSwyLjEgNDIuNDUsMi43OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDEiIGNsYXNzPSJmaWwxMDEiIHBvaW50cz0iMjAuMTgsMTkuODMgNDIuMzQsMi42NSA0Mi44NywzLjM1ICIvPgogICAgPHBvbHlnb24gaWQ9IjEwMiIgY2xhc3M9ImZpbDEwMiIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Mi43NywzLjIxIDQzLjI4LDMuOTIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTAzIiBjbGFzcz0iZmlsMTAzIiBwb2ludHM9IjIwLjE4LDE5LjgzIDQzLjE4LDMuNzcgNDMuNjgsNC40OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDQiIGNsYXNzPSJmaWwxMDQiIHBvaW50cz0iMjAuMTgsMTkuODMgNDMuNTgsNC4zNSA0NC4wNiw1LjA4ICIvPgogICAgPHBvbHlnb24gaWQ9IjEwNSIgY2xhc3M9ImZpbDEwNSIgcG9pbnRzPSIyMC4xOCwxOS44MyA0My45Niw0Ljk0IDQ0LjQyLDUuNjggIi8+CiAgICA8cG9seWdvbiBpZD0iMTA2IiBjbGFzcz0iZmlsMTA2IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ0LjMzLDUuNTMgNDQuNzcsNi4yOSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDciIGNsYXNzPSJmaWwxMDciIHBvaW50cz0iMjAuMTgsMTkuODMgNDQuNjgsNi4xMyA0NS4xMSw2LjkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTA4IiBjbGFzcz0iZmlsMTA4IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ1LjAyLDYuNzUgNDUuNDMsNy41MiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDkiIGNsYXNzPSJmaWwxMDkiIHBvaW50cz0iMjAuMTgsMTkuODMgNDUuMzUsNy4zNyA0NS43NCw4LjE1ICIvPgogICAgPHBvbHlnb24gaWQ9IjExMCIgY2xhc3M9ImZpbDExMCIgcG9pbnRzPSIyMC4xOCwxOS44MyA0NS42Niw3Ljk5IDQ2LjAzLDguNzkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTExIiBjbGFzcz0iZmlsMTExIiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ1Ljk1LDguNjMgNDYuMyw5LjQzICIvPgogICAgPHBvbHlnb24gaWQ9IjExMiIgY2xhc3M9ImZpbDExMiIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ni4yMyw5LjI3IDQ2LjU2LDEwLjA4ICIvPgogICAgPHBvbHlnb24gaWQ9IjExMyIgY2xhc3M9ImZpbDExMyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ni41LDkuOTIgNDYuODEsMTAuNzMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTE0IiBjbGFzcz0iZmlsMTE0IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ2Ljc0LDEwLjU3IDQ3LjAzLDExLjM5ICIvPgogICAgPHBvbHlnb24gaWQ9IjExNSIgY2xhc3M9ImZpbDExNSIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ni45OCwxMS4yMyA0Ny4yNCwxMi4wNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMTYiIGNsYXNzPSJmaWwxMTYiIHBvaW50cz0iMjAuMTgsMTkuODMgNDcuMTksMTEuODkgNDcuNDQsMTIuNzMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTE3IiBjbGFzcz0iZmlsMTE3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ3LjM5LDEyLjU2IDQ3LjYyLDEzLjQgIi8+CiAgICA8cG9seWdvbiBpZD0iMTE4IiBjbGFzcz0iZmlsMTE4IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ3LjU3LDEzLjIzIDQ3Ljc4LDE0LjA4ICIvPgogICAgPHBvbHlnb24gaWQ9IjExOSIgY2xhc3M9ImZpbDExOSIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ny43NCwxMy45MSA0Ny45MywxNC43NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjAiIGNsYXNzPSJmaWwxMjAiIHBvaW50cz0iMjAuMTgsMTkuODMgNDcuODksMTQuNTkgNDguMDUsMTUuNDUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTIxIiBjbGFzcz0iZmlsMTIxIiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjAyLDE1LjI4IDQ4LjE3LDE2LjEzICIvPgogICAgPHBvbHlnb24gaWQ9IjEyMiIgY2xhc3M9ImZpbDEyMiIgcG9pbnRzPSIyMC4xOCwxOS44MyA0OC4xNCwxNS45NiA0OC4yNiwxNi44MiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjMiIGNsYXNzPSJmaWwxMjMiIHBvaW50cz0iMjAuMTgsMTkuODMgNDguMjQsMTYuNjUgNDguMzQsMTcuNTIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTI0IiBjbGFzcz0iZmlsMTI0IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjMyLDE3LjM0IDQ4LjQsMTguMjEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTI1IiBjbGFzcz0iZmlsMTI1IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjM4LDE4LjA0IDQ4LjQ1LDE4LjkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTI2IiBjbGFzcz0iZmlsMTI2IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjQzLDE4LjczIDQ4LjQ3LDE5LjYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTI3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjQ2LDE5LjQyIDQ4LjQ4LDIwLjI5ICIvPgogICAgPHBvbHlnb24gaWQ9IjEyOCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0OC40OCwyMC4xMiA0OC40OCwyMC45OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDguNDgsMjAuODEgNDguNDUsMjEuNjggIi8+CiAgICA8cG9seWdvbiBpZD0iMTMwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjQ2LDIxLjUgNDguNDEsMjIuMzcgIi8+CiAgICA8cG9seWdvbiBpZD0iMTMxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjQyLDIyLjIgNDguMzUsMjMuMDYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTMyIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ4LjM3LDIyLjg5IDQ4LjI4LDIzLjc1ICIvPgogICAgPHBvbHlnb24gaWQ9IjEzMyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0OC4zLDIzLjU4IDQ4LjE5LDI0LjQ0ICIvPgogICAgPHBvbHlnb24gaWQ9IjEzNCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0OC4yMSwyNC4yNiA0OC4wOCwyNS4xMiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMzUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDguMSwyNC45NSA0Ny45NSwyNS44ICIvPgogICAgPHBvbHlnb24gaWQ9IjEzNiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ny45OCwyNS42MyA0Ny44MSwyNi40OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMzciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDcuODQsMjYuMzEgNDcuNjUsMjcuMTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTM4IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ3LjY5LDI2Ljk4IDQ3LjQ4LDI3LjgyICIvPgogICAgPHBvbHlnb24gaWQ9IjEzOSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ny41MiwyNy42NSA0Ny4yOCwyOC40OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDAiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDcuMzMsMjguMzIgNDcuMDcsMjkuMTQgIi8+CiAgICA8cG9seWdvbiBpZD0iMTQxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ3LjEzLDI4Ljk4IDQ2Ljg1LDI5Ljc5ICIvPgogICAgPHBvbHlnb24gaWQ9IjE0MiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ni45MSwyOS42MyA0Ni42MSwzMC40NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDYuNjcsMzAuMjggNDYuMzUsMzEuMDggIi8+CiAgICA8cG9seWdvbiBpZD0iMTQ0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ2LjQyLDMwLjkyIDQ2LjA4LDMxLjcyICIvPgogICAgPHBvbHlnb24gaWQ9IjE0NSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0Ni4xNSwzMS41NiA0NS43OSwzMi4zNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDUuODYsMzIuMTggNDUuNDksMzIuOTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTQ3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ1LjU3LDMyLjgxIDQ1LjE3LDMzLjU3ICIvPgogICAgPHBvbHlnb24gaWQ9IjE0OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0NS4yNSwzMy40MiA0NC44NCwzNC4xNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDQuOTIsMzQuMDIgNDQuNDksMzQuNzcgIi8+CiAgICA8cG9seWdvbiBpZD0iMTUwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQ0LjU4LDM0LjYyIDQ0LjEzLDM1LjM1ICIvPgogICAgPHBvbHlnb24gaWQ9IjE1MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0NC4yMiwzNS4yMSA0My43NSwzNS45MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNTIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDMuODQsMzUuNzggNDMuMzYsMzYuNSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNTMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDMuNDYsMzYuMzUgNDIuOTUsMzcuMDUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTU0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQzLjA1LDM2LjkxIDQyLjUzLDM3LjYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTU1IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQyLjY0LDM3LjQ2IDQyLjEsMzguMTMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTU2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQyLjIxLDM4IDQxLjY1LDM4LjY2ICIvPgogICAgPHBvbHlnb24gaWQ9IjE1NyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0MS43NywzOC41MiA0MS4yLDM5LjE3ICIvPgogICAgPHBvbHlnb24gaWQ9IjE1OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA0MS4zMSwzOS4wNCA0MC43MiwzOS42NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNTkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNDAuODQsMzkuNTQgNDAuMjQsNDAuMTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTYwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQwLjM2LDQwLjA0IDM5Ljc0LDQwLjY0ICIvPgogICAgPHBvbHlnb24gaWQ9IjE2MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzOS44Nyw0MC41MiAzOS4yNCw0MS4xICIvPgogICAgPHBvbHlnb24gaWQ9IjE2MiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzOS4zNiw0MC45OCAzOC43Miw0MS41NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNjMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMzguODUsNDEuNDQgMzguMTksNDEuOTkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTY0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDM4LjMyLDQxLjg4IDM3LjY1LDQyLjQxICIvPgogICAgPHBvbHlnb24gaWQ9IjE2NSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzNy43OCw0Mi4zMSAzNy4wOSw0Mi44MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNjYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMzcuMjMsNDIuNzIgMzYuNTMsNDMuMjIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTY3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDM2LjY3LDQzLjEyIDM1Ljk2LDQzLjYxICIvPgogICAgPHBvbHlnb24gaWQ9IjE2OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzNi4xLDQzLjUxIDM1LjM4LDQzLjk4ICIvPgogICAgPHBvbHlnb24gaWQ9IjE2OSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzNS41Miw0My44OCAzNC43OSw0NC4zMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNzAiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMzQuOTMsNDQuMjQgMzQuMTksNDQuNjcgIi8+CiAgICA8cG9seWdvbiBpZD0iMTcxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDM0LjM0LDQ0LjU4IDMzLjU4LDQ0Ljk5ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3MiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzMy43Myw0NC45MSAzMi45Niw0NS4zICIvPgogICAgPHBvbHlnb24gaWQ9IjE3MyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzMy4xMiw0NS4yMyAzMi4zNCw0NS42ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3NCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzMi41LDQ1LjUyIDMxLjcxLDQ1Ljg4ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3NSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzMS44Nyw0NS44MSAzMS4wNyw0Ni4xNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNzYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMzEuMjMsNDYuMDcgMzAuNDMsNDYuMzkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTc3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDMwLjU5LDQ2LjMyIDI5Ljc4LDQ2LjYyICIvPgogICAgPHBvbHlnb24gaWQ9IjE3OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyOS45NCw0Ni41NiAyOS4xMiw0Ni44MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNzkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMjkuMjksNDYuNzggMjguNDYsNDcuMDMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTgwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDI4LjYyLDQ2Ljk4IDI3Ljc5LDQ3LjIyICIvPgogICAgPHBvbHlnb24gaWQ9IjE4MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyNy45Niw0Ny4xNyAyNy4xMiw0Ny4zOCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMjcuMjksNDcuMzQgMjYuNDUsNDcuNTMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTgzIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDI2LjYxLDQ3LjQ5IDI1Ljc3LDQ3LjY2ICIvPgogICAgPHBvbHlnb24gaWQ9IjE4NCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyNS45NCw0Ny42MyAyNS4wOCw0Ny43OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMjUuMjUsNDcuNzUgMjQuNCw0Ny44OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMjQuNTcsNDcuODUgMjMuNzEsNDcuOTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTg3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDIzLjg4LDQ3Ljk0IDIzLjAyLDQ4LjAzICIvPgogICAgPHBvbHlnb24gaWQ9IjE4OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyMy4xOSw0OC4wMSAyMi4zMyw0OC4wNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMjIuNSw0OC4wNiAyMS42NCw0OC4xICIvPgogICAgPHBvbHlnb24gaWQ9IjE5MCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyMS44MSw0OC4xIDIwLjk0LDQ4LjEyICIvPgogICAgPHBvbHlnb24gaWQ9IjE5MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyMS4xMSw0OC4xMSAyMC4yNSw0OC4xMiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOTIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMjAuNDIsNDguMTIgMTkuNTUsNDguMSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOTMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMTkuNzMsNDguMSAxOC44Niw0OC4wNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOTQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMTkuMDMsNDguMDcgMTguMTYsNDggIi8+CiAgICA8cG9seWdvbiBpZD0iMTk1IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDE4LjM0LDQ4LjAyIDE3LjQ3LDQ3LjkzICIvPgogICAgPHBvbHlnb24gaWQ9IjE5NiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAxNy42NSw0Ny45NSAxNi43OCw0Ny44NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOTciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMTYuOTUsNDcuODcgMTYuMDksNDcuNzQgIi8+CiAgICA8cG9seWdvbiBpZD0iMTk4IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDE2LjI3LDQ3Ljc3IDE1LjQxLDQ3LjYyICIvPgogICAgPHBvbHlnb24gaWQ9IjE5OSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAxNS41OCw0Ny42NSAxNC43Miw0Ny40OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDAiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMTQuOSw0Ny41MSAxNC4wNCw0Ny4zMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDEiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMTQuMjEsNDcuMzYgMTMuMzcsNDcuMTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjAyIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDEzLjU0LDQ3LjIgMTIuNyw0Ni45NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMTIuODYsNDcuMDEgMTIuMDMsNDYuNzYgIi8+CiAgICA8cG9seWdvbiBpZD0iMjA0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDEyLjIsNDYuODEgMTEuMzcsNDYuNTQgIi8+CiAgICA8cG9seWdvbiBpZD0iMjA1IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDExLjUzLDQ2LjYgMTAuNzEsNDYuMzEgIi8+CiAgICA8cG9seWdvbiBpZD0iMjA2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDEwLjg3LDQ2LjM2IDEwLjA2LDQ2LjA1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIwNyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAxMC4yMiw0Ni4xMSA5LjQxLDQ1Ljc4ICIvPgogICAgPHBvbHlnb24gaWQ9IjIwOCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA5LjU3LDQ1Ljg1IDguNzcsNDUuNSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgOC45Myw0NS41NyA4LjE0LDQ1LjIgIi8+CiAgICA8cG9seWdvbiBpZD0iMjEwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDguMyw0NS4yNyA3LjUxLDQ0Ljg5ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxMSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA3LjY3LDQ0Ljk2IDYuOSw0NC41NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMTIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNy4wNSw0NC42NCA2LjI5LDQ0LjIxICIvPgogICAgPHBvbHlnb24gaWQ9IjIxMyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA2LjQ0LDQ0LjMgNS42OSw0My44NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMTQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNS44NCw0My45NCA1LjA5LDQzLjQ4ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxNSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyA1LjI0LDQzLjU3IDQuNTEsNDMuMDkgIi8+CiAgICA8cG9seWdvbiBpZD0iMjE2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDQuNjYsNDMuMTkgMy45NCw0Mi42OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMTciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgNC4wOCw0Mi43OSAzLjM3LDQyLjI3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxOCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAzLjUyLDQyLjM3IDIuODIsNDEuODQgIi8+CiAgICA8cG9seWdvbiBpZD0iMjE5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDIuOTYsNDEuOTUgMi4yOCw0MS40ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyMCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAyLjQxLDQxLjUxIDEuNzQsNDAuOTQgIi8+CiAgICA8cG9seWdvbiBpZD0iMjIxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIDEuODgsNDEuMDYgMS4yMiw0MC40NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMS4zNSw0MC41OSAwLjcxLDM5Ljk5ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyMyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAwLjg0LDQwLjExIDAuMjEsMzkuNSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgMC4zNCwzOS42MiAtMC4yNywzOSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTAuMTUsMzkuMTIgLTAuNzUsMzguNDggIi8+CiAgICA8cG9seWdvbiBpZD0iMjI2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC0wLjYzLDM4LjYxIC0xLjIxLDM3Ljk1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyNyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMS4wOSwzOC4wOCAtMS42NiwzNy40MSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTEuNTQsMzcuNTUgLTIuMDksMzYuODYgIi8+CiAgICA8cG9seWdvbiBpZD0iMjI5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC0xLjk4LDM3IC0yLjUxLDM2LjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjMwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC0yLjQxLDM2LjQ0IC0yLjkyLDM1LjczICIvPgogICAgPHBvbHlnb24gaWQ9IjIzMSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMi44MiwzNS44OCAtMy4zMiwzNS4xNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMzIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTMuMjIsMzUuMyAtMy43LDM0LjU3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzMyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMy42LDM0LjcxIC00LjA2LDMzLjk3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzNCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtMy45NywzNC4xMiAtNC40MSwzMy4zNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMzUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTQuMzIsMzMuNTIgLTQuNzUsMzIuNzUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjM2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC00LjY2LDMyLjkgLTUuMDcsMzIuMTMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjM3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC00Ljk5LDMyLjI4IC01LjM4LDMxLjUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjM4IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC01LjMsMzEuNjYgLTUuNjcsMzAuODYgIi8+CiAgICA8cG9seWdvbiBpZD0iMjM5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC01LjU5LDMxLjAyIC01Ljk0LDMwLjIyICIvPgogICAgPHBvbHlnb24gaWQ9IjI0MCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNS44NywzMC4zOCAtNi4yLDI5LjU3ICIvPgogICAgPHBvbHlnb24gaWQ9IjI0MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNi4xNCwyOS43MyAtNi40NCwyOC45MiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTYuMzgsMjkuMDggLTYuNjcsMjguMjYgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQzIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC02LjYxLDI4LjQyIC02Ljg4LDI3LjU5ICIvPgogICAgPHBvbHlnb24gaWQ9IjI0NCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNi44MywyNy43NiAtNy4wOCwyNi45MiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuMDMsMjcuMDkgLTcuMjYsMjYuMjUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQ2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC03LjIxLDI2LjQyIC03LjQyLDI1LjU3ICIvPgogICAgPHBvbHlnb24gaWQ9IjI0NyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNy4zOCwyNS43NCAtNy41NiwyNC44OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuNTMsMjUuMDYgLTcuNjksMjQuMiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTcuNjYsMjQuMzcgLTcuODEsMjMuNTIgIi8+CiAgICA8cG9seWdvbiBpZD0iMjUwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC03Ljc4LDIzLjY5IC03LjksMjIuODMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjUxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC03Ljg4LDIzIC03Ljk4LDIyLjE0ICIvPgogICAgPHBvbHlnb24gaWQ9IjI1MiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyMC4xOCwxOS44MyAtNy45NiwyMi4zMSAtOC4wNCwyMS40NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNTMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjAuMTgsMTkuODMgLTguMDIsMjEuNjIgLTguMDgsMjAuNzUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjU0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjIwLjE4LDE5LjgzIC04LjA3LDIwLjkyIC04LjExLDIwLjA1ICIvPgogICAgPHBvbHlnb24gaWQ9IjI1NSIgY2xhc3M9ImZpbDEyOCIgcG9pbnRzPSIyMC4xOCwxOS44MyAtOC4xLDIwLjIzIC04LjEyLDE5LjUzICIvPgogICA8L2c+CiAgPC9nPgogPC9nPgo8L3N2Zz4=") no-repeat;
}
html.theme-dark .large-2qn7A4BC .circleWrapper-2qn7A4BC {
    background-image:url("data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbDpzcGFjZT0icHJlc2VydmUiIHdpZHRoPSIzMTZweCIgaGVpZ2h0PSIxNThweCIgdmVyc2lvbj0iMS4xIiBzdHlsZT0ic2hhcGUtcmVuZGVyaW5nOmdlb21ldHJpY1ByZWNpc2lvbjsgdGV4dC1yZW5kZXJpbmc6Z2VvbWV0cmljUHJlY2lzaW9uOyBpbWFnZS1yZW5kZXJpbmc6b3B0aW1pemVRdWFsaXR5OyBmaWxsLXJ1bGU6ZXZlbm9kZDsgY2xpcC1ydWxlOmV2ZW5vZGQiCnZpZXdCb3g9IjAgMCA1Ny4wNiAyOC41MyIKIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIj4KIDxkZWZzPgogIDxzdHlsZSB0eXBlPSJ0ZXh0L2NzcyI+CiAgIDwhW0NEQVRBWwogICAgLmZpbDY0IHtmaWxsOiMwMEIyQzZ9CiAgICAuZmlsNjMge2ZpbGw6IzAwQjJDOH0KICAgIC5maWw2NyB7ZmlsbDojMDBCM0MwfQogICAgLmZpbDY2IHtmaWxsOiMwMEIzQzJ9CiAgICAuZmlsNjUge2ZpbGw6IzAwQjNDNH0KICAgIC5maWw3MCB7ZmlsbDojMDBCNEJCfQogICAgLmZpbDY5IHtmaWxsOiMwMEI0QkR9CiAgICAuZmlsNjgge2ZpbGw6IzAwQjRCRn0KICAgIC5maWw3MyB7ZmlsbDojMDBCNUI2fQogICAgLmZpbDcyIHtmaWxsOiMwMEI1Qjh9CiAgICAuZmlsNzEge2ZpbGw6IzAwQjVCOX0KICAgIC5maWw3NiB7ZmlsbDojMDBCNkIxfQogICAgLmZpbDc1IHtmaWxsOiMwMEI2QjJ9CiAgICAuZmlsNzQge2ZpbGw6IzAwQjZCNH0KICAgIC5maWw3OSB7ZmlsbDojMDBCN0FCfQogICAgLmZpbDc4IHtmaWxsOiMwMEI3QUR9CiAgICAuZmlsNzcge2ZpbGw6IzAwQjdBRn0KICAgIC5maWw4MiB7ZmlsbDojMDBCOEE2fQogICAgLmZpbDgxIHtmaWxsOiMwMEI4QTh9CiAgICAuZmlsODAge2ZpbGw6IzAwQjhBOX0KICAgIC5maWw4NSB7ZmlsbDojMDBCOUExfQogICAgLmZpbDg0IHtmaWxsOiMwMEI5QTJ9CiAgICAuZmlsODMge2ZpbGw6IzAwQjlBNH0KICAgIC5maWw4OCB7ZmlsbDojMDBCQTlCfQogICAgLmZpbDg3IHtmaWxsOiMwMEJBOUR9CiAgICAuZmlsODYge2ZpbGw6IzAwQkE5Rn0KICAgIC5maWw5MSB7ZmlsbDojMDBCQjk2fQogICAgLmZpbDkwIHtmaWxsOiMwMEJCOTh9CiAgICAuZmlsODkge2ZpbGw6IzAwQkI5OX0KICAgIC5maWw5NCB7ZmlsbDojMDBCQzkxfQogICAgLmZpbDkzIHtmaWxsOiMwMEJDOTJ9CiAgICAuZmlsOTIge2ZpbGw6IzAwQkM5NH0KICAgIC5maWw5NyB7ZmlsbDojMDBCRDhCfQogICAgLmZpbDk2IHtmaWxsOiMwMEJEOER9CiAgICAuZmlsOTUge2ZpbGw6IzAwQkQ4Rn0KICAgIC5maWwxMDAge2ZpbGw6IzAwQkU4Nn0KICAgIC5maWw5OSB7ZmlsbDojMDBCRTg4fQogICAgLmZpbDk4IHtmaWxsOiMwMEJFOEF9CiAgICAuZmlsMTAzIHtmaWxsOiMwMEJGODF9CiAgICAuZmlsMTAyIHtmaWxsOiMwMEJGODJ9CiAgICAuZmlsMTAxIHtmaWxsOiMwMEJGODR9CiAgICAuZmlsMTA2IHtmaWxsOiMwMEMwN0J9CiAgICAuZmlsMTA1IHtmaWxsOiMwMEMwN0R9CiAgICAuZmlsMTA0IHtmaWxsOiMwMEMwN0Z9CiAgICAuZmlsMTA5IHtmaWxsOiMwMEMxNzZ9CiAgICAuZmlsMTA4IHtmaWxsOiMwMEMxNzh9CiAgICAuZmlsMTA3IHtmaWxsOiMwMEMxN0F9CiAgICAuZmlsMTEyIHtmaWxsOiMwMEMyNzF9CiAgICAuZmlsMTExIHtmaWxsOiMwMEMyNzJ9CiAgICAuZmlsMTEwIHtmaWxsOiMwMEMyNzR9CiAgICAuZmlsMTE1IHtmaWxsOiMwMEMzNkJ9CiAgICAuZmlsMTE0IHtmaWxsOiMwMEMzNkR9CiAgICAuZmlsMTEzIHtmaWxsOiMwMEMzNkZ9CiAgICAuZmlsMTE4IHtmaWxsOiMwMEM0NjZ9CiAgICAuZmlsMTE3IHtmaWxsOiMwMEM0Njh9CiAgICAuZmlsMTE2IHtmaWxsOiMwMEM0NkF9CiAgICAuZmlsMTIxIHtmaWxsOiMwMEM1NjF9CiAgICAuZmlsMTIwIHtmaWxsOiMwMEM1NjN9CiAgICAuZmlsMTE5IHtmaWxsOiMwMEM1NjR9CiAgICAuZmlsMTI0IHtmaWxsOiMwMEM2NUJ9CiAgICAuZmlsMTIzIHtmaWxsOiMwMEM2NUR9CiAgICAuZmlsMTIyIHtmaWxsOiMwMEM2NUZ9CiAgICAuZmlsMTI3IHtmaWxsOiMwMEM3NTd9CiAgICAuZmlsMTI2IHtmaWxsOiMwMEM3NTh9CiAgICAuZmlsMTI1IHtmaWxsOiMwMEM3NUF9CiAgICAuZmlsNjIge2ZpbGw6IzAzQjBDNn0KICAgIC5maWw2MSB7ZmlsbDojMDdBREM0fQogICAgLmZpbDYwIHtmaWxsOiMwQkFBQzJ9CiAgICAuZmlsNTkge2ZpbGw6IzBGQThDMH0KICAgIC5maWw1OCB7ZmlsbDojMTNBNUJFfQogICAgLmZpbDU3IHtmaWxsOiMxN0EyQkN9CiAgICAuZmlsNTYge2ZpbGw6IzFCOUZCQX0KICAgIC5maWw1NSB7ZmlsbDojMUY5Q0I3fQogICAgLmZpbDU0IHtmaWxsOiMyMzlBQjV9CiAgICAuZmlsNTMge2ZpbGw6IzI3OTdCM30KICAgIC5maWw1MiB7ZmlsbDojMkI5NEIxfQogICAgLmZpbDUxIHtmaWxsOiMyRjkxQUZ9CiAgICAuZmlsNTAge2ZpbGw6IzMzOEVBRH0KICAgIC5maWw0OSB7ZmlsbDojMzc4Q0FCfQogICAgLmZpbDQ4IHtmaWxsOiMzQjg5QTl9CiAgICAuZmlsNDcge2ZpbGw6IzNGODZBNn0KICAgIC5maWw0NiB7ZmlsbDojNDM4M0E0fQogICAgLmZpbDQ1IHtmaWxsOiM0NzgwQTJ9CiAgICAuZmlsNDQge2ZpbGw6IzRCN0VBMH0KICAgIC5maWw0MyB7ZmlsbDojNEY3QjlFfQogICAgLmZpbDQyIHtmaWxsOiM1Mzc4OUN9CiAgICAuZmlsNDEge2ZpbGw6IzU3NzU5QX0KICAgIC5maWw0MCB7ZmlsbDojNUI3Mjk3fQogICAgLmZpbDM5IHtmaWxsOiM1RjcwOTV9CiAgICAuZmlsMzgge2ZpbGw6IzYzNkQ5M30KICAgIC5maWwzNyB7ZmlsbDojNjc2QTkxfQogICAgLmZpbDM2IHtmaWxsOiM2QjY3OEZ9CiAgICAuZmlsMzUge2ZpbGw6IzZGNjU4RH0KICAgIC5maWwzNCB7ZmlsbDojNzM2MjhCfQogICAgLmZpbDMzIHtmaWxsOiM3NzVGODl9CiAgICAuZmlsMzIge2ZpbGw6IzdCNUM4Nn0KICAgIC5maWwzMSB7ZmlsbDojN0Y1OTg0fQogICAgLmZpbDMwIHtmaWxsOiM4MzU3ODJ9CiAgICAuZmlsMjkge2ZpbGw6Izg3NTQ4MH0KICAgIC5maWwyOCB7ZmlsbDojOEI1MTdFfQogICAgLmZpbDI3IHtmaWxsOiM4RjRFN0N9CiAgICAuZmlsMjYge2ZpbGw6IzkzNEI3QX0KICAgIC5maWwyNSB7ZmlsbDojOTc0OTc3fQogICAgLmZpbDI0IHtmaWxsOiM5QjQ2NzV9CiAgICAuZmlsMjMge2ZpbGw6IzlGNDM3M30KICAgIC5maWwyMiB7ZmlsbDojQTM0MDcxfQogICAgLmZpbDIxIHtmaWxsOiNBNzNENkZ9CiAgICAuZmlsMjAge2ZpbGw6I0FCM0I2RH0KICAgIC5maWwxOSB7ZmlsbDojQUYzODZCfQogICAgLmZpbDE4IHtmaWxsOiNCMzM1Njl9CiAgICAuZmlsMTcge2ZpbGw6I0I3MzI2Nn0KICAgIC5maWwxNiB7ZmlsbDojQkIyRjY0fQogICAgLmZpbDE1IHtmaWxsOiNCRjJENjJ9CiAgICAuZmlsMTQge2ZpbGw6I0MzMkE2MH0KICAgIC5maWwxMyB7ZmlsbDojQzcyNzVFfQogICAgLmZpbDEyIHtmaWxsOiNDQjI0NUN9CiAgICAuZmlsMTEge2ZpbGw6I0NGMjI1QX0KICAgIC5maWwxMCB7ZmlsbDojRDMxRjU3fQogICAgLmZpbDkge2ZpbGw6I0Q3MUM1NX0KICAgIC5maWw4IHtmaWxsOiNEQjE5NTN9CiAgICAuZmlsNyB7ZmlsbDojREYxNjUxfQogICAgLmZpbDYge2ZpbGw6I0UzMTQ0Rn0KICAgIC5maWw1IHtmaWxsOiNFNzExNER9CiAgICAuZmlsNCB7ZmlsbDojRUIwRTRCfQogICAgLmZpbDMge2ZpbGw6I0VGMEI0OX0KICAgIC5maWwyIHtmaWxsOiNGMzA4NDZ9CiAgICAuZmlsMSB7ZmlsbDojRjcwNjQ0fQogICAgLmZpbDAge2ZpbGw6I0ZCMDM0Mn0KICAgIC5maWwxMjgge2ZpbGw6I0ZGMDA0MH0KICAgXV0+CiAgPC9zdHlsZT4KICAgIDxjbGlwUGF0aCBpZD0iaWQwIj4KICAgICA8cGF0aCBkPSJNNS4wMyAxMi4zNWMwLjA2LC0wLjA5IDAuMTcsLTAuMTUgMC4yOSwtMC4xNSAwLjA4LDAgMC4xNSwwLjAyIDAuMjEsMC4wNyAwLjE2LDAuMTEgMC4yLDAuMzQgMC4wOSwwLjUgLTMuMTMsNC41MyAtNC44NCw5LjkgLTQuOSwxNS40IDAsMC4yIC0wLjE2LDAuMzYgLTAuMzYsMC4zNiAtMC4yLDAgLTAuMzYsLTAuMTYgLTAuMzYsLTAuMzYgMCwwIDAsMCAwLDAgMC4wNywtNS44NyAxLjkyLC0xMS4zMSA1LjAzLC0xNS44MmwwIDB6bTQ2LjUgLTAuMDhjLTAuMDksMC4wNyAtMC4xNSwwLjE4IC0wLjE1LDAuMjkgMCwwLjA4IDAuMDIsMC4xNSAwLjA2LDAuMjEgMy4xMyw0LjUzIDQuODQsOS45IDQuOSwxNS40IDAsMC4yIDAuMTYsMC4zNiAwLjM2LDAuMzYgMC4yLDAgMC4zNiwtMC4xNiAwLjM2LC0wLjM2IDAsMCAwLDAgMCwwIC0wLjA1LC01LjY1IC0xLjgxLC0xMS4xNiAtNS4wMiwtMTUuODIgLTAuMDcsLTAuMDkgLTAuMTgsLTAuMTUgLTAuMywtMC4xNSAtMC4wNywwIC0wLjE1LDAuMDIgLTAuMjEsMC4wN2wwIDB6bS0xMy42MyAtOS45M2MtMC4xNSwtMC4wNSAtMC4yNCwtMC4xOSAtMC4yNCwtMC4zNCAwLC0wLjA0IDAsLTAuMDggMC4wMiwtMC4xMiAwLjA0LC0wLjE0IDAuMTgsLTAuMjQgMC4zNCwtMC4yNCAwLjA0LDAgMC4wOCwwIDAuMTEsMC4wMiA1LjE3LDEuODUgOS43MSw1LjE2IDEzLjA1LDkuNTIgMC4xMiwwLjE2IDAuMDksMC4zOSAtMC4wOCwwLjUgLTAuMDYsMC4wNSAtMC4xMywwLjA3IC0wLjIxLDAuMDcgLTAuMTEsMCAtMC4yMiwtMC4wNSAtMC4yOSwtMC4xNCAtMy4yNSwtNC4yNCAtNy42NywtNy40NiAtMTIuNywtOS4yN2wwIDB6bS0xNy44MyAtMC42OGMwLjA1LDAuMTUgMC4xOSwwLjI1IDAuMzUsMC4yNSAwLjAzLDAgMC4wNywtMC4wMSAwLjEsLTAuMDIgMi41OSwtMC43NyA1LjI4LC0xLjE3IDcuOTksLTEuMTcgMCwwIDAuMDEsMCAwLjAyLDAgMi43OCwwIDUuNDcsMC40MSA4LjAxLDEuMTcgMC4wMywwLjAxIDAuMDcsMC4wMiAwLjEsMC4wMiAwLjE2LDAgMC4zLC0wLjEgMC4zNSwtMC4yNSAwLjAxLC0wLjA0IDAuMDIsLTAuMDggMC4wMiwtMC4xMiAwLC0wLjE1IC0wLjExLC0wLjI5IC0wLjI2LC0wLjM0IC0yLjY1LC0wLjc5IC01LjQyLC0xLjIgLTguMTksLTEuMiAtMC4wMSwwIC0wLjAyLDAgLTAuMDMsMCAtMi44NiwwIC01LjYyLDAuNDIgLTguMjIsMS4yIC0wLjE1LDAuMDUgLTAuMjUsMC4xOSAtMC4yNSwwLjM0IDAsMC4wNCAwLDAuMDggMC4wMSwwLjEybDAgMHptLTAuNjggMC4yMmMwLjAxLDAuMDQgMC4wMiwwLjA4IDAuMDIsMC4xMiAwLDAuMTUgLTAuMSwwLjI5IC0wLjI1LDAuMzQgLTUuMDMsMS44IC05LjQ1LDUuMDMgLTEyLjcsOS4yNyAtMC4wNywwLjA5IC0wLjE4LDAuMTQgLTAuMjksMC4xNCAtMC4wOCwwIC0wLjE1LC0wLjAyIC0wLjIxLC0wLjA3IC0wLjEsLTAuMDYgLTAuMTUsLTAuMTcgLTAuMTUsLTAuMjkgMCwtMC4wNyAwLjAzLC0wLjE1IDAuMDcsLTAuMjEgMy4zNCwtNC4zNiA3Ljg4LC03LjY3IDEzLjA1LC05LjUyIDAuMTksLTAuMDcgMC4zOSwwLjAzIDAuNDYsMC4yMmwwIDB6Ii8+CiAgICA8L2NsaXBQYXRoPgogPC9kZWZzPgogPGcgaWQ9IjEiPgogIDxnPgogICA8ZyBzdHlsZT0iY2xpcC1wYXRoOnVybCgjaWQwKSI+CiAgICA8cG9seWdvbiBjbGFzcz0iZmlsMCIgcG9pbnRzPSIyOC45OSwyOC40OCAtMTEuNjYsMjguMzEgLTExLjY2LDI2LjgxICIvPgogICAgPHBvbHlnb24gaWQ9IjEiIGNsYXNzPSJmaWwxIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMS42NiwyNy4wNiAtMTEuNjIsMjUuODEgIi8+CiAgICA8cG9seWdvbiBpZD0iMiIgY2xhc3M9ImZpbDIiIHBvaW50cz0iMjguOTksMjguNDggLTExLjYzLDI2LjA2IC0xMS41NiwyNC44MiAiLz4KICAgIDxwb2x5Z29uIGlkPSIzIiBjbGFzcz0iZmlsMyIgcG9pbnRzPSIyOC45OSwyOC40OCAtMTEuNTgsMjUuMDcgLTExLjQ4LDIzLjgzICIvPgogICAgPHBvbHlnb24gaWQ9IjQiIGNsYXNzPSJmaWw0IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMS41LDI0LjA4IC0xMS4zNywyMi44NCAiLz4KICAgIDxwb2x5Z29uIGlkPSI1IiBjbGFzcz0iZmlsNSIgcG9pbnRzPSIyOC45OSwyOC40OCAtMTEuNCwyMy4wOSAtMTEuMjQsMjEuODUgIi8+CiAgICA8cG9seWdvbiBpZD0iNiIgY2xhc3M9ImZpbDYiIHBvaW50cz0iMjguOTksMjguNDggLTExLjI3LDIyLjEgLTExLjA4LDIwLjg3ICIvPgogICAgPHBvbHlnb24gaWQ9IjciIGNsYXNzPSJmaWw3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMS4xMiwyMS4xMiAtMTAuOSwxOS44OSAiLz4KICAgIDxwb2x5Z29uIGlkPSI4IiBjbGFzcz0iZmlsOCIgcG9pbnRzPSIyOC45OSwyOC40OCAtMTAuOTUsMjAuMTQgLTEwLjcsMTguOTIgIi8+CiAgICA8cG9seWdvbiBpZD0iOSIgY2xhc3M9ImZpbDkiIHBvaW50cz0iMjguOTksMjguNDggLTEwLjc1LDE5LjE2IC0xMC40NywxNy45NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMCIgY2xhc3M9ImZpbDEwIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMC41MywxOC4yIC0xMC4yMiwxNi45OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMSIgY2xhc3M9ImZpbDExIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMC4yOCwxNy4yMyAtOS45NCwxNi4wNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMiIgY2xhc3M9ImZpbDEyIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMC4wMSwxNi4yOCAtOS42NCwxNS4xICIvPgogICAgPHBvbHlnb24gaWQ9IjEzIiBjbGFzcz0iZmlsMTMiIHBvaW50cz0iMjguOTksMjguNDggLTkuNzIsMTUuMzMgLTkuMzIsMTQuMTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTQiIGNsYXNzPSJmaWwxNCIgcG9pbnRzPSIyOC45OSwyOC40OCAtOS40LDE0LjM5IC04Ljk4LDEzLjIzICIvPgogICAgPHBvbHlnb24gaWQ9IjE1IiBjbGFzcz0iZmlsMTUiIHBvaW50cz0iMjguOTksMjguNDggLTkuMDYsMTMuNDYgLTguNjEsMTIuMzEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTYiIGNsYXNzPSJmaWwxNiIgcG9pbnRzPSIyOC45OSwyOC40OCAtOC43LDEyLjU0IC04LjIyLDExLjQgIi8+CiAgICA8cG9seWdvbiBpZD0iMTciIGNsYXNzPSJmaWwxNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtOC4zMSwxMS42MyAtNy44LDEwLjUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTgiIGNsYXNzPSJmaWwxOCIgcG9pbnRzPSIyOC45OSwyOC40OCAtNy45MSwxMC43MiAtNy4zNyw5LjYxICIvPgogICAgPHBvbHlnb24gaWQ9IjE5IiBjbGFzcz0iZmlsMTkiIHBvaW50cz0iMjguOTksMjguNDggLTcuNDgsOS44MyAtNi45MSw4LjczICIvPgogICAgPHBvbHlnb24gaWQ9IjIwIiBjbGFzcz0iZmlsMjAiIHBvaW50cz0iMjguOTksMjguNDggLTcuMDIsOC45NSAtNi40Myw3Ljg3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxIiBjbGFzcz0iZmlsMjEiIHBvaW50cz0iMjguOTksMjguNDggLTYuNTUsOC4wOCAtNS45Myw3LjAxICIvPgogICAgPHBvbHlnb24gaWQ9IjIyIiBjbGFzcz0iZmlsMjIiIHBvaW50cz0iMjguOTksMjguNDggLTYuMDUsNy4yMyAtNS40MSw2LjE3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzIiBjbGFzcz0iZmlsMjMiIHBvaW50cz0iMjguOTksMjguNDggLTUuNTQsNi4zOCAtNC44Nyw1LjM0ICIvPgogICAgPHBvbHlnb24gaWQ9IjI0IiBjbGFzcz0iZmlsMjQiIHBvaW50cz0iMjguOTksMjguNDggLTUsNS41NSAtNC4zLDQuNTMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjUiIGNsYXNzPSJmaWwyNSIgcG9pbnRzPSIyOC45OSwyOC40OCAtNC40NCw0Ljc0IC0zLjcyLDMuNzMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjYiIGNsYXNzPSJmaWwyNiIgcG9pbnRzPSIyOC45OSwyOC40OCAtMy44NywzLjkzIC0zLjEyLDIuOTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjciIGNsYXNzPSJmaWwyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtMy4yNywzLjE1IC0yLjUsMi4xOCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyOCIgY2xhc3M9ImZpbDI4IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0yLjY1LDIuMzcgLTEuODYsMS40MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyOSIgY2xhc3M9ImZpbDI5IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0yLjAyLDEuNjIgLTEuMiwwLjY5ICIvPgogICAgPHBvbHlnb24gaWQ9IjMwIiBjbGFzcz0iZmlsMzAiIHBvaW50cz0iMjguOTksMjguNDggLTEuMzYsMC44OCAtMC41MiwtMC4wMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIzMSIgY2xhc3M9ImZpbDMxIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0wLjY5LDAuMTUgMC4xNywtMC43MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIzMiIgY2xhc3M9ImZpbDMyIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDAsLTAuNTUgMC44OSwtMS40MSAiLz4KICAgIDxwb2x5Z29uIGlkPSIzMyIgY2xhc3M9ImZpbDMzIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDAuNzEsLTEuMjQgMS42MiwtMi4wOCAiLz4KICAgIDxwb2x5Z29uIGlkPSIzNCIgY2xhc3M9ImZpbDM0IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDEuNDMsLTEuOTEgMi4zNiwtMi43MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIzNSIgY2xhc3M9ImZpbDM1IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDIuMTgsLTIuNTcgMy4xMiwtMy4zNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIzNiIgY2xhc3M9ImZpbDM2IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDIuOTMsLTMuMiAzLjksLTMuOTcgIi8+CiAgICA8cG9seWdvbiBpZD0iMzciIGNsYXNzPSJmaWwzNyIgcG9pbnRzPSIyOC45OSwyOC40OCAzLjcxLC0zLjgyIDQuNjksLTQuNTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMzgiIGNsYXNzPSJmaWwzOCIgcG9pbnRzPSIyOC45OSwyOC40OCA0LjUsLTQuNDEgNS41LC01LjEzICIvPgogICAgPHBvbHlnb24gaWQ9IjM5IiBjbGFzcz0iZmlsMzkiIHBvaW50cz0iMjguOTksMjguNDggNS4zLC00Ljk5IDYuMzIsLTUuNjggIi8+CiAgICA8cG9seWdvbiBpZD0iNDAiIGNsYXNzPSJmaWw0MCIgcG9pbnRzPSIyOC45OSwyOC40OCA2LjEyLC01LjU0IDcuMTYsLTYuMjEgIi8+CiAgICA8cG9seWdvbiBpZD0iNDEiIGNsYXNzPSJmaWw0MSIgcG9pbnRzPSIyOC45OSwyOC40OCA2Ljk1LC02LjA4IDguMDEsLTYuNzIgIi8+CiAgICA8cG9seWdvbiBpZD0iNDIiIGNsYXNzPSJmaWw0MiIgcG9pbnRzPSIyOC45OSwyOC40OCA3Ljc5LC02LjU5IDguODcsLTcuMjEgIi8+CiAgICA8cG9seWdvbiBpZD0iNDMiIGNsYXNzPSJmaWw0MyIgcG9pbnRzPSIyOC45OSwyOC40OCA4LjY1LC03LjA5IDkuNzQsLTcuNjggIi8+CiAgICA8cG9seWdvbiBpZD0iNDQiIGNsYXNzPSJmaWw0NCIgcG9pbnRzPSIyOC45OSwyOC40OCA5LjUyLC03LjU2IDEwLjYyLC04LjEyICIvPgogICAgPHBvbHlnb24gaWQ9IjQ1IiBjbGFzcz0iZmlsNDUiIHBvaW50cz0iMjguOTksMjguNDggMTAuNCwtOC4wMSAxMS41MiwtOC41NCAiLz4KICAgIDxwb2x5Z29uIGlkPSI0NiIgY2xhc3M9ImZpbDQ2IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDExLjMsLTguNDQgMTIuNDMsLTguOTQgIi8+CiAgICA8cG9seWdvbiBpZD0iNDciIGNsYXNzPSJmaWw0NyIgcG9pbnRzPSIyOC45OSwyOC40OCAxMi4yLC04Ljg0IDEzLjM0LC05LjMyICIvPgogICAgPHBvbHlnb24gaWQ9IjQ4IiBjbGFzcz0iZmlsNDgiIHBvaW50cz0iMjguOTksMjguNDggMTMuMTEsLTkuMjMgMTQuMjcsLTkuNjggIi8+CiAgICA8cG9seWdvbiBpZD0iNDkiIGNsYXNzPSJmaWw0OSIgcG9pbnRzPSIyOC45OSwyOC40OCAxNC4wNCwtOS41OSAxNS4yLC0xMC4wMSAiLz4KICAgIDxwb2x5Z29uIGlkPSI1MCIgY2xhc3M9ImZpbDUwIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDE0Ljk3LC05LjkyIDE2LjE0LC0xMC4zMiAiLz4KICAgIDxwb2x5Z29uIGlkPSI1MSIgY2xhc3M9ImZpbDUxIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDE1LjkxLC0xMC4yNCAxNy4wOSwtMTAuNiAiLz4KICAgIDxwb2x5Z29uIGlkPSI1MiIgY2xhc3M9ImZpbDUyIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDE2Ljg2LC0xMC41MyAxOC4wNSwtMTAuODcgIi8+CiAgICA8cG9seWdvbiBpZD0iNTMiIGNsYXNzPSJmaWw1MyIgcG9pbnRzPSIyOC45OSwyOC40OCAxNy44MSwtMTAuOCAxOS4wMiwtMTEuMSAiLz4KICAgIDxwb2x5Z29uIGlkPSI1NCIgY2xhc3M9ImZpbDU0IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDE4Ljc4LC0xMS4wNCAxOS45OSwtMTEuMzIgIi8+CiAgICA8cG9seWdvbiBpZD0iNTUiIGNsYXNzPSJmaWw1NSIgcG9pbnRzPSIyOC45OSwyOC40OCAxOS43NCwtMTEuMjYgMjAuOTYsLTExLjUxICIvPgogICAgPHBvbHlnb24gaWQ9IjU2IiBjbGFzcz0iZmlsNTYiIHBvaW50cz0iMjguOTksMjguNDggMjAuNzIsLTExLjQ2IDIxLjk0LC0xMS42OCAiLz4KICAgIDxwb2x5Z29uIGlkPSI1NyIgY2xhc3M9ImZpbDU3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDIxLjcsLTExLjYzIDIyLjkzLC0xMS44MiAiLz4KICAgIDxwb2x5Z29uIGlkPSI1OCIgY2xhc3M9ImZpbDU4IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDIyLjY4LC0xMS43OCAyMy45MiwtMTEuOTQgIi8+CiAgICA8cG9seWdvbiBpZD0iNTkiIGNsYXNzPSJmaWw1OSIgcG9pbnRzPSIyOC45OSwyOC40OCAyMy42NywtMTEuOSAyNC45MSwtMTIuMDMgIi8+CiAgICA8cG9seWdvbiBpZD0iNjAiIGNsYXNzPSJmaWw2MCIgcG9pbnRzPSIyOC45OSwyOC40OCAyNC42NiwtMTIgMjUuOSwtMTIuMSAiLz4KICAgIDxwb2x5Z29uIGlkPSI2MSIgY2xhc3M9ImZpbDYxIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI1LjY1LC0xMi4wOCAyNi45LC0xMi4xNCAiLz4KICAgIDxwb2x5Z29uIGlkPSI2MiIgY2xhc3M9ImZpbDYyIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI2LjY1LC0xMi4xMyAyNy44OSwtMTIuMTYgIi8+CiAgICA8cG9seWdvbiBpZD0iNjMiIGNsYXNzPSJmaWw2MyIgcG9pbnRzPSIyOC45OSwyOC40OCAyNy42NCwtMTIuMTYgMjguODksLTEyLjE2ICIvPgogICAgPHBvbHlnb24gaWQ9IjY0IiBjbGFzcz0iZmlsNjQiIHBvaW50cz0iMjguOTksMjguNDggMjguNjQsLTEyLjE2IDI5Ljg5LC0xMi4xMyAiLz4KICAgIDxwb2x5Z29uIGlkPSI2NSIgY2xhc3M9ImZpbDY1IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI5LjY0LC0xMi4xNCAzMC44OSwtMTIuMDggIi8+CiAgICA8cG9seWdvbiBpZD0iNjYiIGNsYXNzPSJmaWw2NiIgcG9pbnRzPSIyOC45OSwyOC40OCAzMC42NCwtMTIuMDkgMzEuODgsLTEyICIvPgogICAgPHBvbHlnb24gaWQ9IjY3IiBjbGFzcz0iZmlsNjciIHBvaW50cz0iMjguOTksMjguNDggMzEuNjMsLTEyLjAyIDMyLjg4LC0xMS45ICIvPgogICAgPHBvbHlnb24gaWQ9IjY4IiBjbGFzcz0iZmlsNjgiIHBvaW50cz0iMjguOTksMjguNDggMzIuNjMsLTExLjkyIDMzLjg3LC0xMS43NyAiLz4KICAgIDxwb2x5Z29uIGlkPSI2OSIgY2xhc3M9ImZpbDY5IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDMzLjYyLC0xMS44IDM0Ljg2LC0xMS42MiAiLz4KICAgIDxwb2x5Z29uIGlkPSI3MCIgY2xhc3M9ImZpbDcwIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDM0LjYxLC0xMS42NiAzNS44NCwtMTEuNDUgIi8+CiAgICA8cG9seWdvbiBpZD0iNzEiIGNsYXNzPSJmaWw3MSIgcG9pbnRzPSIyOC45OSwyOC40OCAzNS42LC0xMS40OSAzNi44MiwtMTEuMjUgIi8+CiAgICA8cG9seWdvbiBpZD0iNzIiIGNsYXNzPSJmaWw3MiIgcG9pbnRzPSIyOC45OSwyOC40OCAzNi41OCwtMTEuMyAzNy44LC0xMS4wMyAiLz4KICAgIDxwb2x5Z29uIGlkPSI3MyIgY2xhc3M9ImZpbDczIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDM3LjU2LC0xMS4wOCAzOC43NywtMTAuNzggIi8+CiAgICA8cG9seWdvbiBpZD0iNzQiIGNsYXNzPSJmaWw3NCIgcG9pbnRzPSIyOC45OSwyOC40OCAzOC41MywtMTAuODQgMzkuNzQsLTEwLjUxICIvPgogICAgPHBvbHlnb24gaWQ9Ijc1IiBjbGFzcz0iZmlsNzUiIHBvaW50cz0iMjguOTksMjguNDggMzkuNSwtMTAuNTcgNDAuNywtMTAuMjIgIi8+CiAgICA8cG9seWdvbiBpZD0iNzYiIGNsYXNzPSJmaWw3NiIgcG9pbnRzPSIyOC45OSwyOC40OCA0MC40NiwtMTAuMjkgNDEuNjUsLTkuOSAiLz4KICAgIDxwb2x5Z29uIGlkPSI3NyIgY2xhc3M9ImZpbDc3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQxLjQxLC05Ljk4IDQyLjU5LC05LjU2ICIvPgogICAgPHBvbHlnb24gaWQ9Ijc4IiBjbGFzcz0iZmlsNzgiIHBvaW50cz0iMjguOTksMjguNDggNDIuMzYsLTkuNjQgNDMuNTMsLTkuMiAiLz4KICAgIDxwb2x5Z29uIGlkPSI3OSIgY2xhc3M9ImZpbDc5IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQzLjI5LC05LjI4IDQ0LjQ2LC04LjgxICIvPgogICAgPHBvbHlnb24gaWQ9IjgwIiBjbGFzcz0iZmlsODAiIHBvaW50cz0iMjguOTksMjguNDggNDQuMjIsLTguOTEgNDUuMzcsLTguNCAiLz4KICAgIDxwb2x5Z29uIGlkPSI4MSIgY2xhc3M9ImZpbDgxIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQ1LjE0LC04LjUgNDYuMjgsLTcuOTcgIi8+CiAgICA8cG9seWdvbiBpZD0iODIiIGNsYXNzPSJmaWw4MiIgcG9pbnRzPSIyOC45OSwyOC40OCA0Ni4wNSwtOC4wOCA0Ny4xOCwtNy41MiAiLz4KICAgIDxwb2x5Z29uIGlkPSI4MyIgY2xhc3M9ImZpbDgzIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQ2Ljk1LC03LjYzIDQ4LjA3LC03LjA1ICIvPgogICAgPHBvbHlnb24gaWQ9Ijg0IiBjbGFzcz0iZmlsODQiIHBvaW50cz0iMjguOTksMjguNDggNDcuODQsLTcuMTYgNDguOTQsLTYuNTUgIi8+CiAgICA8cG9seWdvbiBpZD0iODUiIGNsYXNzPSJmaWw4NSIgcG9pbnRzPSIyOC45OSwyOC40OCA0OC43MiwtNi42NyA0OS44LC02LjAzICIvPgogICAgPHBvbHlnb24gaWQ9Ijg2IiBjbGFzcz0iZmlsODYiIHBvaW50cz0iMjguOTksMjguNDggNDkuNTksLTYuMTYgNTAuNjUsLTUuNSAiLz4KICAgIDxwb2x5Z29uIGlkPSI4NyIgY2xhc3M9ImZpbDg3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDUwLjQ0LC01LjYzIDUxLjQ5LC00Ljk0ICIvPgogICAgPHBvbHlnb24gaWQ9Ijg4IiBjbGFzcz0iZmlsODgiIHBvaW50cz0iMjguOTksMjguNDggNTEuMjgsLTUuMDggNTIuMzIsLTQuMzYgIi8+CiAgICA8cG9seWdvbiBpZD0iODkiIGNsYXNzPSJmaWw4OSIgcG9pbnRzPSIyOC45OSwyOC40OCA1Mi4xMSwtNC41IDUzLjEzLC0zLjc2ICIvPgogICAgPHBvbHlnb24gaWQ9IjkwIiBjbGFzcz0iZmlsOTAiIHBvaW50cz0iMjguOTksMjguNDggNTIuOTIsLTMuOTEgNTMuOTIsLTMuMTUgIi8+CiAgICA8cG9seWdvbiBpZD0iOTEiIGNsYXNzPSJmaWw5MSIgcG9pbnRzPSIyOC45OSwyOC40OCA1My43MiwtMy4zIDU0LjcsLTIuNTEgIi8+CiAgICA8cG9seWdvbiBpZD0iOTIiIGNsYXNzPSJmaWw5MiIgcG9pbnRzPSIyOC45OSwyOC40OCA1NC41MSwtMi42NyA1NS40NywtMS44NiAiLz4KICAgIDxwb2x5Z29uIGlkPSI5MyIgY2xhc3M9ImZpbDkzIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDU1LjI4LC0yLjAyIDU2LjIyLC0xLjE4ICIvPgogICAgPHBvbHlnb24gaWQ9Ijk0IiBjbGFzcz0iZmlsOTQiIHBvaW50cz0iMjguOTksMjguNDggNTYuMDMsLTEuMzUgNTYuOTUsLTAuNDkgIi8+CiAgICA8cG9seWdvbiBpZD0iOTUiIGNsYXNzPSJmaWw5NSIgcG9pbnRzPSIyOC45OSwyOC40OCA1Ni43NiwtMC42NiA1Ny42NiwwLjIyICIvPgogICAgPHBvbHlnb24gaWQ9Ijk2IiBjbGFzcz0iZmlsOTYiIHBvaW50cz0iMjguOTksMjguNDggNTcuNDgsMC4wNCA1OC4zNiwwLjk0ICIvPgogICAgPHBvbHlnb24gaWQ9Ijk3IiBjbGFzcz0iZmlsOTciIHBvaW50cz0iMjguOTksMjguNDggNTguMTksMC43NiA1OS4wNCwxLjY4ICIvPgogICAgPHBvbHlnb24gaWQ9Ijk4IiBjbGFzcz0iZmlsOTgiIHBvaW50cz0iMjguOTksMjguNDggNTguODcsMS41IDU5LjcxLDIuNDQgIi8+CiAgICA8cG9seWdvbiBpZD0iOTkiIGNsYXNzPSJmaWw5OSIgcG9pbnRzPSIyOC45OSwyOC40OCA1OS41NCwyLjI1IDYwLjM1LDMuMjEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTAwIiBjbGFzcz0iZmlsMTAwIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDYwLjE5LDMuMDIgNjAuOTgsNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDEiIGNsYXNzPSJmaWwxMDEiIHBvaW50cz0iMjguOTksMjguNDggNjAuODIsMy44MSA2MS41OCw0LjgxICIvPgogICAgPHBvbHlnb24gaWQ9IjEwMiIgY2xhc3M9ImZpbDEwMiIgcG9pbnRzPSIyOC45OSwyOC40OCA2MS40Myw0LjYxIDYyLjE3LDUuNjIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTAzIiBjbGFzcz0iZmlsMTAzIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDYyLjAyLDUuNDIgNjIuNzMsNi40NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDQiIGNsYXNzPSJmaWwxMDQiIHBvaW50cz0iMjguOTksMjguNDggNjIuNTksNi4yNSA2My4yOCw3LjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTA1IiBjbGFzcz0iZmlsMTA1IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDYzLjE0LDcuMDkgNjMuODEsOC4xNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDYiIGNsYXNzPSJmaWwxMDYiIHBvaW50cz0iMjguOTksMjguNDggNjMuNjcsNy45NSA2NC4zMSw5LjAzICIvPgogICAgPHBvbHlnb24gaWQ9IjEwNyIgY2xhc3M9ImZpbDEwNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2NC4xOCw4LjgxIDY0Ljc5LDkuOTEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTA4IiBjbGFzcz0iZmlsMTA4IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY0LjY3LDkuNjkgNjUuMjYsMTAuOCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMDkiIGNsYXNzPSJmaWwxMDkiIHBvaW50cz0iMjguOTksMjguNDggNjUuMTQsMTAuNTggNjUuNjksMTEuNzEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTEwIiBjbGFzcz0iZmlsMTEwIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY1LjU4LDExLjQ4IDY2LjExLDEyLjYyICIvPgogICAgPHBvbHlnb24gaWQ9IjExMSIgY2xhc3M9ImZpbDExMSIgcG9pbnRzPSIyOC45OSwyOC40OCA2Ni4wMSwxMi4zOSA2Ni41MSwxMy41NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMTIiIGNsYXNzPSJmaWwxMTIiIHBvaW50cz0iMjguOTksMjguNDggNjYuNDEsMTMuMzEgNjYuODgsMTQuNDggIi8+CiAgICA8cG9seWdvbiBpZD0iMTEzIiBjbGFzcz0iZmlsMTEzIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY2Ljc5LDE0LjI0IDY3LjIzLDE1LjQyICIvPgogICAgPHBvbHlnb24gaWQ9IjExNCIgY2xhc3M9ImZpbDExNCIgcG9pbnRzPSIyOC45OSwyOC40OCA2Ny4xNCwxNS4xOCA2Ny41NiwxNi4zNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMTUiIGNsYXNzPSJmaWwxMTUiIHBvaW50cz0iMjguOTksMjguNDggNjcuNDcsMTYuMTMgNjcuODYsMTcuMzIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTE2IiBjbGFzcz0iZmlsMTE2IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY3Ljc4LDE3LjA4IDY4LjE0LDE4LjI4ICIvPgogICAgPHBvbHlnb24gaWQ9IjExNyIgY2xhc3M9ImZpbDExNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2OC4wNywxOC4wNCA2OC40LDE5LjI1ICIvPgogICAgPHBvbHlnb24gaWQ9IjExOCIgY2xhc3M9ImZpbDExOCIgcG9pbnRzPSIyOC45OSwyOC40OCA2OC4zMywxOS4wMSA2OC42MywyMC4yMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMTkiIGNsYXNzPSJmaWwxMTkiIHBvaW50cz0iMjguOTksMjguNDggNjguNTcsMTkuOTggNjguODQsMjEuMiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjAiIGNsYXNzPSJmaWwxMjAiIHBvaW50cz0iMjguOTksMjguNDggNjguNzksMjAuOTYgNjkuMDIsMjIuMTkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTIxIiBjbGFzcz0iZmlsMTIxIiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY4Ljk4LDIxLjk0IDY5LjE4LDIzLjE4ICIvPgogICAgPHBvbHlnb24gaWQ9IjEyMiIgY2xhc3M9ImZpbDEyMiIgcG9pbnRzPSIyOC45OSwyOC40OCA2OS4xNCwyMi45MyA2OS4zMiwyNC4xNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjMiIGNsYXNzPSJmaWwxMjMiIHBvaW50cz0iMjguOTksMjguNDggNjkuMjksMjMuOTIgNjkuNDMsMjUuMTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTI0IiBjbGFzcz0iZmlsMTI0IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY5LjQsMjQuOTEgNjkuNTIsMjYuMTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTI1IiBjbGFzcz0iZmlsMTI1IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY5LjUsMjUuOSA2OS41OSwyNy4xNSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjYiIGNsYXNzPSJmaWwxMjYiIHBvaW50cz0iMjguOTksMjguNDggNjkuNTcsMjYuOSA2OS42MiwyOC4xNSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjkuNjEsMjcuOSA2OS42NCwyOS4xNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjkuNjMsMjguOSA2OS42MywzMC4xNCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMjkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjkuNjMsMjkuODkgNjkuNTksMzEuMTQgIi8+CiAgICA8cG9seWdvbiBpZD0iMTMwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY5LjYsMzAuODkgNjkuNTQsMzIuMTMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTMxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY5LjU1LDMxLjg4IDY5LjQ1LDMzLjEyICIvPgogICAgPHBvbHlnb24gaWQ9IjEzMiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2OS40NywzMi44OCA2OS4zNCwzNC4xMSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMzMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjkuMzcsMzMuODcgNjkuMjEsMzUuMSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMzQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjkuMjQsMzQuODUgNjkuMDYsMzYuMDggIi8+CiAgICA8cG9seWdvbiBpZD0iMTM1IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY5LjA5LDM1Ljg0IDY4Ljg4LDM3LjA2ICIvPgogICAgPHBvbHlnb24gaWQ9IjEzNiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2OC45MiwzNi44MSA2OC42NywzOC4wMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxMzciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjguNzIsMzcuNzkgNjguNDQsMzkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTM4IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY4LjUsMzguNzYgNjguMTksMzkuOTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTM5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY4LjI1LDM5LjcyIDY3LjkyLDQwLjkxICIvPgogICAgPHBvbHlnb24gaWQ9IjE0MCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2Ny45OCw0MC42NyA2Ny42Miw0MS44NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDEiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjcuNjksNDEuNjIgNjcuMjksNDIuOCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjcuMzcsNDIuNTYgNjYuOTUsNDMuNzIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTQzIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY3LjAzLDQzLjQ5IDY2LjU4LDQ0LjY0ICIvPgogICAgPHBvbHlnb24gaWQ9IjE0NCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2Ni42Nyw0NC40MSA2Ni4xOSw0NS41NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjYuMjksNDUuMzMgNjUuNzgsNDYuNDUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTQ2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDY1Ljg4LDQ2LjIzIDY1LjM0LDQ3LjM0ICIvPgogICAgPHBvbHlnb24gaWQ9IjE0NyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2NS40NSw0Ny4xMiA2NC44OCw0OC4yMiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjUsNDggNjQuNCw0OS4wOSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNDkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjQuNTIsNDguODcgNjMuOSw0OS45NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNTAiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjQuMDMsNDkuNzMgNjMuMzgsNTAuNzggIi8+CiAgICA8cG9seWdvbiBpZD0iMTUxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDYzLjUxLDUwLjU3IDYyLjg0LDUxLjYxICIvPgogICAgPHBvbHlnb24gaWQ9IjE1MiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2Mi45Nyw1MS40IDYyLjI4LDUyLjQyICIvPgogICAgPHBvbHlnb24gaWQ9IjE1MyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2Mi40Miw1Mi4yMiA2MS43LDUzLjIyICIvPgogICAgPHBvbHlnb24gaWQ9IjE1NCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA2MS44NCw1My4wMiA2MS4wOSw1NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNTUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNjEuMjQsNTMuODEgNjAuNDcsNTQuNzcgIi8+CiAgICA8cG9seWdvbiBpZD0iMTU2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDYwLjYzLDU0LjU4IDU5LjgzLDU1LjUyICIvPgogICAgPHBvbHlnb24gaWQ9IjE1NyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA1OS45OSw1NS4zNCA1OS4xNyw1Ni4yNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNTgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNTkuMzQsNTYuMDggNTguNDksNTYuOTggIi8+CiAgICA8cG9seWdvbiBpZD0iMTU5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDU4LjY2LDU2LjggNTcuOCw1Ny42OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNjAiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNTcuOTcsNTcuNTEgNTcuMDksNTguMzcgIi8+CiAgICA8cG9seWdvbiBpZD0iMTYxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDU3LjI2LDU4LjE5IDU2LjM2LDU5LjAzICIvPgogICAgPHBvbHlnb24gaWQ9IjE2MiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA1Ni41NCw1OC44NyA1NS42MSw1OS42OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNjMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNTUuOCw1OS41MiA1NC44NSw2MC4zMSAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNjQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNTUuMDQsNjAuMTUgNTQuMDcsNjAuOTIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTY1IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDU0LjI3LDYwLjc3IDUzLjI4LDYxLjUxICIvPgogICAgPHBvbHlnb24gaWQ9IjE2NiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA1My40OCw2MS4zNiA1Mi40Nyw2Mi4wOCAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNjciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNTIuNjcsNjEuOTQgNTEuNjUsNjIuNjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTY4IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDUxLjg2LDYyLjUgNTAuODIsNjMuMTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTY5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDUxLjAyLDYzLjAzIDQ5Ljk3LDYzLjY3ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3MCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA1MC4xOCw2My41NSA0OS4xMSw2NC4xNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNzEiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNDkuMzIsNjQuMDQgNDguMjMsNjQuNjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTcyIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQ4LjQ1LDY0LjUxIDQ3LjM1LDY1LjA3ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3MyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA0Ny41Nyw2NC45NiA0Ni40NSw2NS41ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3NCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA0Ni42OCw2NS4zOSA0NS41NSw2NS45ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3NSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA0NS43Nyw2NS43OSA0NC42Myw2Ni4yNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNzYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNDQuODYsNjYuMTggNDMuNzEsNjYuNjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMTc3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQzLjk0LDY2LjU0IDQyLjc3LDY2Ljk2ICIvPgogICAgPHBvbHlnb24gaWQ9IjE3OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA0Myw2Ni44OCA0MS44Myw2Ny4yNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxNzkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNDIuMDYsNjcuMTkgNDAuODgsNjcuNTYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTgwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDQxLjEyLDY3LjQ4IDM5LjkyLDY3LjgyICIvPgogICAgPHBvbHlnb24gaWQ9IjE4MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA0MC4xNiw2Ny43NSAzOC45Niw2OC4wNiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMzkuMiw2OCAzNy45OSw2OC4yNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMzguMjMsNjguMjIgMzcuMDEsNjguNDYgIi8+CiAgICA8cG9seWdvbiBpZD0iMTg0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDM3LjI1LDY4LjQxIDM2LjAzLDY4LjYzICIvPgogICAgPHBvbHlnb24gaWQ9IjE4NSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAzNi4yOCw2OC41OCAzNS4wNSw2OC43NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxODYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMzUuMjksNjguNzMgMzQuMDYsNjguODkgIi8+CiAgICA8cG9seWdvbiBpZD0iMTg3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDM0LjMsNjguODYgMzMuMDcsNjguOTggIi8+CiAgICA8cG9seWdvbiBpZD0iMTg4IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDMzLjMxLDY4Ljk2IDMyLjA3LDY5LjA1ICIvPgogICAgPHBvbHlnb24gaWQ9IjE4OSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAzMi4zMiw2OS4wMyAzMS4wOCw2OS4xICIvPgogICAgPHBvbHlnb24gaWQ9IjE5MCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAzMS4zMyw2OS4wOCAzMC4wOCw2OS4xMiAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOTEiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMzAuMzMsNjkuMTEgMjkuMDgsNjkuMTEgIi8+CiAgICA8cG9seWdvbiBpZD0iMTkyIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI5LjMzLDY5LjExIDI4LjA4LDY5LjA4ICIvPgogICAgPHBvbHlnb24gaWQ9IjE5MyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAyOC4zMyw2OS4wOSAyNy4wOSw2OS4wMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIxOTQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMjcuMzQsNjkuMDQgMjYuMDksNjguOTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTk1IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI2LjM0LDY4Ljk3IDI1LjEsNjguODUgIi8+CiAgICA8cG9seWdvbiBpZD0iMTk2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI1LjM1LDY4Ljg3IDI0LjEsNjguNzIgIi8+CiAgICA8cG9seWdvbiBpZD0iMTk3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDI0LjM1LDY4Ljc1IDIzLjEyLDY4LjU3ICIvPgogICAgPHBvbHlnb24gaWQ9IjE5OCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAyMy4zNiw2OC42MSAyMi4xMyw2OC40ICIvPgogICAgPHBvbHlnb24gaWQ9IjE5OSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAyMi4zOCw2OC40NCAyMS4xNSw2OC4yICIvPgogICAgPHBvbHlnb24gaWQ9IjIwMCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAyMS4zOSw2OC4yNSAyMC4xNyw2Ny45OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDEiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMjAuNDIsNjguMDMgMTkuMiw2Ny43MyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMTkuNDQsNjcuNzkgMTguMjQsNjcuNDYgIi8+CiAgICA8cG9seWdvbiBpZD0iMjAzIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDE4LjQ4LDY3LjUzIDE3LjI4LDY3LjE3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIwNCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAxNy41Miw2Ny4yNCAxNi4zMyw2Ni44NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMTYuNTYsNjYuOTMgMTUuMzgsNjYuNTEgIi8+CiAgICA8cG9seWdvbiBpZD0iMjA2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDE1LjYyLDY2LjU5IDE0LjQ0LDY2LjE1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIwNyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAxNC42OCw2Ni4yNCAxMy41Miw2NS43NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMTMuNzUsNjUuODYgMTIuNiw2NS4zNSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMDkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMTIuODMsNjUuNDYgMTEuNjksNjQuOTIgIi8+CiAgICA8cG9seWdvbiBpZD0iMjEwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDExLjkyLDY1LjAzIDEwLjc5LDY0LjQ3ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxMSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAxMS4wMiw2NC41OCA5LjkxLDY0ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxMiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAxMC4xMyw2NC4xMiA5LjAzLDYzLjUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjEzIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDkuMjUsNjMuNjMgOC4xNyw2Mi45OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMTQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggOC4zOSw2My4xMSA3LjMyLDYyLjQ1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIxNSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA3LjUzLDYyLjU4IDYuNDgsNjEuODkgIi8+CiAgICA8cG9seWdvbiBpZD0iMjE2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDYuNjksNjIuMDMgNS42Niw2MS4zMSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMTciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNS44Niw2MS40NiA0Ljg1LDYwLjcyICIvPgogICAgPHBvbHlnb24gaWQ9IjIxOCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCA1LjA1LDYwLjg3IDQuMDUsNjAuMSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMTkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggNC4yNSw2MC4yNSAzLjI3LDU5LjQ2ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyMCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAzLjQ3LDU5LjYyIDIuNTEsNTguODEgIi8+CiAgICA8cG9seWdvbiBpZD0iMjIxIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IDIuNyw1OC45NyAxLjc2LDU4LjE0ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyMiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAxLjk0LDU4LjMgMS4wMiw1Ny40NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjMiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggMS4yMSw1Ny42MiAwLjMxLDU2Ljc0ICIvPgogICAgPHBvbHlnb24gaWQ9IjIyNCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAwLjQ5LDU2LjkxIC0wLjM5LDU2LjAxICIvPgogICAgPHBvbHlnb24gaWQ9IjIyNSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtMC4yMSw1Ni4xOSAtMS4wNyw1NS4yNyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjYiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTAuOSw1NS40NSAtMS43Myw1NC41MSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjciIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTEuNTcsNTQuNyAtMi4zOCw1My43NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMjgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTIuMjIsNTMuOTMgLTMsNTIuOTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjI5IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0yLjg1LDUzLjE1IC0zLjYxLDUyLjE1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzMCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtMy40Niw1Mi4zNSAtNC4yLDUxLjMzICIvPgogICAgPHBvbHlnb24gaWQ9IjIzMSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtNC4wNSw1MS41MyAtNC43Niw1MC41ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzMiIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtNC42Miw1MC43IC01LjMxLDQ5LjY1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzMyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtNS4xNyw0OS44NiAtNS44Myw0OC43OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMzQiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTUuNyw0OS4wMSAtNi4zNCw0Ny45MiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMzUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTYuMjEsNDguMTQgLTYuODIsNDcuMDQgIi8+CiAgICA8cG9seWdvbiBpZD0iMjM2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC02LjcsNDcuMjYgLTcuMjgsNDYuMTUgIi8+CiAgICA8cG9seWdvbiBpZD0iMjM3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC03LjE3LDQ2LjM3IC03LjcyLDQ1LjI1ICIvPgogICAgPHBvbHlnb24gaWQ9IjIzOCIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtNy42MSw0NS40NyAtOC4xNCw0NC4zMyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyMzkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTguMDMsNDQuNTYgLTguNTMsNDMuNDEgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQwIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC04LjQzLDQzLjY0IC04LjkxLDQyLjQ4ICIvPgogICAgPHBvbHlnb24gaWQ9IjI0MSIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtOC44MSw0Mi43MSAtOS4yNiw0MS41NCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTkuMTcsNDEuNzcgLTkuNTgsNDAuNTkgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQzIiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC05LjUsNDAuODIgLTkuODksMzkuNjMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQ0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC05LjgxLDM5Ljg3IC0xMC4xNywzOC42NyAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDUiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTEwLjEsMzguOTEgLTEwLjQyLDM3LjcgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQ2IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMC4zNiwzNy45NCAtMTAuNjYsMzYuNzMgIi8+CiAgICA8cG9seWdvbiBpZD0iMjQ3IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMC42LDM2Ljk3IC0xMC44NywzNS43NSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDgiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTEwLjgxLDM1Ljk5IC0xMS4wNSwzNC43NiAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNDkiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTExLDM1LjAxIC0xMS4yMSwzMy43OCAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNTAiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTExLjE3LDM0LjAyIC0xMS4zNSwzMi43OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNTEiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTExLjMxLDMzLjAzIC0xMS40NiwzMS43OSAiLz4KICAgIDxwb2x5Z29uIGlkPSIyNTIiIGNsYXNzPSJmaWwxMjciIHBvaW50cz0iMjguOTksMjguNDggLTExLjQzLDMyLjA0IC0xMS41NSwzMC44ICIvPgogICAgPHBvbHlnb24gaWQ9IjI1MyIgY2xhc3M9ImZpbDEyNyIgcG9pbnRzPSIyOC45OSwyOC40OCAtMTEuNTIsMzEuMDUgLTExLjYxLDI5LjggIi8+CiAgICA8cG9seWdvbiBpZD0iMjU0IiBjbGFzcz0iZmlsMTI3IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMS41OSwzMC4wNSAtMTEuNjUsMjguODEgIi8+CiAgICA8cG9seWdvbiBpZD0iMjU1IiBjbGFzcz0iZmlsMTI4IiBwb2ludHM9IjI4Ljk5LDI4LjQ4IC0xMS42NCwyOS4wNSAtMTEuNjYsMjguMDYgIi8+CiAgIDwvZz4KICA8L2c+CiA8L2c+Cjwvc3ZnPg==");
}
.small-2qn7A4BC .semicircle-2qn7A4BC{
	width:144px;
	height:72px;
	border-top-left-radius:144px;
	border-top-right-radius:144px
}
.small-2qn7A4BC .arrow-2qn7A4BC{
	height:64px
}
.small-2qn7A4BC .arrowMain-2qn7A4BC{
	height:70px
}
.adaptive-2qn7A4BC .speedometerTextWrapper-2qn7A4BC{
	width:56vw;
	left:calc(50%-28vw)
}
.adaptive-2qn7A4BC .middleSignals-2qn7A4BC{
	width:calc(100% + 30px);
	margin-top:5vw
}
.adaptive-2qn7A4BC .bottomSignals-2qn7A4BC{
	width:calc(100% + 100px);
	margin-top:5vw
}
.adaptive-2qn7A4BC .sizeWrapper-2qn7A4BC{
	width:56vw;
	height:28vw
}
.adaptive-2qn7A4BC .circleWrapper-2qn7A4BC{
	width:100%;
	height:100%;
	background-size:cover
}
.adaptive-2qn7A4BC .semicircle-2qn7A4BC{
	top:auto;
	left:6px;
	bottom:0;
	width:calc(100%-12px);
	height:calc(100%-6px);
	border-top-left-radius:100vw;
	border-top-right-radius:100vw
}
.adaptive-2qn7A4BC .arrow-2qn7A4BC{
	height:84%
}
.wrap-3obNZqvj{
	position:relative;
	direction:ltr;
	width:100%;
	height:100%;
	overflow:hidden
}
.wrap-3obNZqvj svg{
	display:block
}
.wrapWithArrowsOuting-3obNZqvj{
	width:calc(100%-40px);
	margin-left:auto;
	margin-right:auto;
	overflow:visible
}
.wrapOverflow-3obNZqvj{
	overflow:hidden;
	height:100%;
	width:100%
}
.scrollWrap-3obNZqvj{
	position:relative;
	width:100%;
	height:100%;
	overflow-x:auto;
	overflow-y:hidden;
	-webkit-overflow-scrolling:touch;
	contain:content
}
.scrollWrap-3obNZqvj::-webkit-scrollbar{
	width:5px;
	height:5px
}
.scrollWrap-3obNZqvj::-webkit-scrollbar-thumb{
	border:1px solid;
	border-color:#f1f3f6;
	border-radius:3px;
	background-color:#d1d4dc
}
html.theme-dark .scrollWrap-3obNZqvj::-webkit-scrollbar-thumb{
	background-color:#50535e;
	border-color:#1e222d
}
.scrollWrap-3obNZqvj::-webkit-scrollbar-track{
	background-color:transparent;
	border-radius:3px
}
.scrollWrap-3obNZqvj::-webkit-scrollbar-corner{
	display:none
}
.scrollWrap-3obNZqvj.noScrollBar-3obNZqvj{
	padding-bottom:100px;
	margin-bottom:-100px;
	-ms-overflow-style:none
}
.scrollWrap-3obNZqvj.noScrollBar-3obNZqvj.sb-scrollbar-wrap{
	display:none
}
.scrollWrap-3obNZqvj.noScrollBar-3obNZqvj::-webkit-scrollbar{
	display:none;
	width:0;
	height:0
}
.scrollWrap-3obNZqvj.noScrollBar-3obNZqvj::-webkit-scrollbar-thumb,.scrollWrap-3obNZqvj.noScrollBar-3obNZqvj::-webkit-scrollbar-track{
	display:none
}
.scrollWrap-3obNZqvj.noScrollBar-3obNZqvj::-webkit-scrollbar-corner{
	display:none
}
.icon-3obNZqvj{
	display:block;
	transition:transform 60ms ease
}
.scrollLeft-3obNZqvj,.scrollRight-3obNZqvj{
	display:flex;
	position:absolute;
	top:0;
	height:100%;
	width:24px;
	background-color:rgba(30,34,45,.6);
	color:#fff;
	transition:background-color .35s ease,transform .11666667s cubic-bezier(.55,.055,.675,.19);
	flex-direction:column;
	justify-content:center;
	align-items:center;
	overflow:hidden
}
html.theme-dark .scrollLeft-3obNZqvj,html.theme-dark .scrollRight-3obNZqvj{
	color:#fff;
	background-color:hsla(227,6%,44%,.6)
}
.scrollLeft-3obNZqvj:active,.scrollRight-3obNZqvj:active{
	transition:background-color 58.33333ms ease,transform .11666667s cubic-bezier(.215,.61,.355,1)
}
@media (any-hover:hover),(min--moz-device-pixel-ratio:0){
	.scrollLeft-3obNZqvj:hover,.scrollRight-3obNZqvj:hover{
		transition:background-color 58.33333ms ease,transform .11666667s cubic-bezier(.215,.61,.355,1)
}
}
.scrollLeft-3obNZqvj:active .icon-3obNZqvj,.scrollRight-3obNZqvj:active .icon-3obNZqvj{
	transform:translateY(1px)
}
@media (any-hover:hover),(min--moz-device-pixel-ratio:0){
	.scrollLeft-3obNZqvj:hover .icon-3obNZqvj,.scrollRight-3obNZqvj:hover .icon-3obNZqvj{
		transform:translateY(1px)
}
}
.scrollLeft-3obNZqvj.isVisible-3obNZqvj,.scrollRight-3obNZqvj.isVisible-3obNZqvj{
	transform:translateX(0);
	transition-timing-function:cubic-bezier(.215,.61,.355,1)
}
.scrollLeft-3obNZqvj{
	left:0;
	transform:translateX(-100%)
}
.scrollLeft-3obNZqvj .iconWrap-3obNZqvj{
	transform:rotate(90deg)
}
.scrollRight-3obNZqvj{
	right:0;
	transform:translateX(100%)
}
.scrollRight-3obNZqvj .iconWrap-3obNZqvj{
	transform:rotate(-90deg)
}
.fadeLeft-3obNZqvj,.fadeRight-3obNZqvj{
	position:absolute;
	pointer-events:none;
	width:50px;
	height:100%;
	top:0
}
.fadeLeft-3obNZqvj.isVisible-3obNZqvj,.fadeRight-3obNZqvj.isVisible-3obNZqvj{
	transform:translateX(0);
	transition-timing-function:cubic-bezier(.215,.61,.355,1)
}
.fadeLeft-3obNZqvj{
	left:0;
	background-image:linear-gradient(270deg,hsla(0,0%,100%,0),#fff);
	transform:translateX(-100%)
}
html.theme-dark .fadeLeft-3obNZqvj{
	background-image:linear-gradient(270deg,rgba(19,23,34,0),#131722)
}
.fadeRight-3obNZqvj{
	right:0;
	background-image:linear-gradient(90deg,hsla(0,0%,100%,0),#fff);
	transform:translateX(100%)
}
html.theme-dark .fadeRight-3obNZqvj{
	background-image:linear-gradient(90deg,rgba(19,23,34,0),#131722)
}
.button-1cy7XKgV{
	display:inline-flex;
	align-items:center;
	justify-content:center;
	border:none;
	outline:none;
	background-color:var(--70B);
	cursor:pointer;
	border-radius:6px;
	color:var(--10B);
	font-family:source sans pro,sans-serif !important;
	font-size:14px !important;
    font-weight:400 !important;
}
html.theme-dark .button-1cy7XKgV{
	color:var(--10B);
	border-radius:30px;
	background-color:var(--70B);
	font-family:source sans pro,sans-serif!important;
    font-weight:400 !important;
	line-height:36px!important;
    padding:0 20px;
}
.button-1cy7XKgV:focus-visible{
	transition:background .2s cubic-bezier(1,0,.16,1)
}
@media (any-hover:hover),(min--moz-device-pixel-ratio:0){
	.button-1cy7XKgV:hover{
		transition:background .2s cubic-bezier(1,0,.16,1)
}
}
@media (any-hover:hover),(min--moz-device-pixel-ratio:0){
	.button-1cy7XKgV.isSelected-1cy7XKgV:hover,.button-1cy7XKgV:hover{
		background-color:var(--HB);
}
}
@media (any-hover:hover),(min--moz-device-pixel-ratio:0){
	html.theme-dark .button-1cy7XKgV.isSelected-1cy7XKgV:hover,html.theme-dark .button-1cy7XKgV:hover{
		background-color:var(--HB);
}
}
.button-1cy7XKgV:focus{
	background-color:var(--HB);
}
html.theme-dark .button-1cy7XKgV:focus{
	background-color:var(--HB);
}
.button-1cy7XKgV.isSelected-1cy7XKgV,.button-1cy7XKgV:active,html.theme-dark .button-1cy7XKgV.isSelected-1cy7XKgV,html.theme-dark .button-1cy7XKgV:active{
	background-color:var(--HB);
}
.button-1cy7XKgV:focus-visible{
	background-color:var(--HB);
}
html.theme-dark .button-1cy7XKgV:focus-visible{
	background-color:var(--HB);
}
.button-1cy7XKgV[disabled]{
	color:#b2b5be;
	background:none
}
html.theme-dark .button-1cy7XKgV[disabled]{
	color:#50535e
}
.medium-1cy7XKgV{
	font-size:16px;
	line-height:24px;
	height:34px;
	min-width:34px;
	padding:0 8px
}
.medium-1cy7XKgV,.small-1cy7XKgV{
	font-weight:400;
	font-style:normal
}
.small-1cy7XKgV{
	font-size:14px;
	line-height:21px;
	height:28px;
	min-width:28px;
	padding:0 6px
}
.scrollButton-1AF3OfzY{
	position:absolute;
	top:0
}
.scrollButton-1AF3OfzY:not(.isVisible-1AF3OfzY){
	display:none
}
.medium-1AF3OfzY,.small-1AF3OfzY{
	padding:0
}
.left-1AF3OfzY{
	left:0
}
.right-1AF3OfzY{
	right:0
}
.right-1AF3OfzY svg{
	transform:scaleX(-1)
}
.tabs-3-f9q69b{
	display:inline-block;
	margin:0 var(--button-tabs-horizontal-scroll-padding,0);
	white-space:nowrap
}
.tabs-3-f9q69b>:not(:first-child){
	margin-left:12px
}
.small-3-f9q69b.leftFade-3-f9q69b{
	--button-tabs-left-fade-width:28px
}
.small-3-f9q69b.rightFade-3-f9q69b{
	--button-tabs-right-fade-width:28px
}
.medium-3-f9q69b.leftFade-3-f9q69b{
	--button-tabs-left-fade-width:34px
}
.medium-3-f9q69b.rightFade-3-f9q69b{
	--button-tabs-right-fade-width:34px
}
.scrollWrapper-3-f9q69b{
	-webkit-mask-image:linear-gradient(90deg,rgba(0,0,0,.05) 0 var(--button-tabs-left-fade-width,0),#000 var(--button-tabs-left-fade-width,0) calc(100%-var(--button-tabs-right-fade-width, 0px)),rgba(0,0,0,.05) calc(100%-var(--button-tabs-right-fade-width, 0px)) 100%);
	mask-image:linear-gradient(90deg,rgba(0,0,0,.05) 0 var(--button-tabs-left-fade-width,0),#000 var(--button-tabs-left-fade-width,0) calc(100%-var(--button-tabs-right-fade-width, 0px)),rgba(0,0,0,.05) calc(100%-var(--button-tabs-right-fade-width, 0px)) 100%)
}
.technicalsTab-DPgs-R4s{
	background-color:#fff;
	padding:25px 25px 40px;
	min-width:480px;
	overflow:auto
}
html.theme-dark .technicalsTab-DPgs-R4s{
	background-color:#1e222d
}
@media screen and (max-width:767px){
	.technicalsTab-DPgs-R4s{
		max-width:100vw;
		box-sizing:border-box;
		padding:20px 20px 38px
}
}
@media screen and (max-width:479px){
	.technicalsTab-DPgs-R4s{
		min-width:0
}
}
.background-DPgs-R4s{
	height:100%;
	width:100%
}
.speedometersContainer-DPgs-R4s{
	display:flex;
	justify-content:space-between;
	align-items:flex-end;
	flex-wrap:wrap;
	margin:20px 20px 11px;
	cursor:default
}
.speedometersContainerNoData-DPgs-R4s{
	height:calc(100%-11px)
}
.alignStart-DPgs-R4s{
	align-items:flex-start
}
.noTopMargin-DPgs-R4s{
	margin-top:1px; /* align title to other widgets */
}
.speedometerWrapper-DPgs-R4s{
	display:flex;
	flex-direction:column;
	align-items:center;
	flex-grow:1;
	order:2;
	min-width:343px;
	contain:content
}
.speedometerTitle-DPgs-R4s{
	margin:30px 16px;
	font-size:24px;
	color:var(--10B);
	letter-spacing:normal;
	font-weight:400;
	text-align:center
}
html.theme-dark .speedometerTitle-DPgs-R4s{
	color:var(--10B);
	font-family:SofiaProRegular,sans-serif;
	font-weight:400!important;
	font-size:24px;
	line-height:30px;
}
.speedometerSignal-DPgs-R4s{
	margin:25px 0 30px;
	font-size:24px;
	text-transform:uppercase;
	letter-spacing:normal;
	font-weight:700
}
.buyColor-DPgs-R4s{
	color:var(--GRN);
}
.sellColor-DPgs-R4s{
	color:var(--RED);
}
.neutralColor-DPgs-R4s{
	color:var(--HB);
}
.countersWrapper-DPgs-R4s{
	display:flex;
	justify-content:space-between
}
.counterWrapper-DPgs-R4s{
	display:flex;
	flex-direction:column;
	align-items:center;
	margin:0 26px
}
.counterNumber-DPgs-R4s{
	font-size:20px;
	margin-bottom:5px
}
.counterTitle-DPgs-R4s{
	font-size:12px;
	color:#131722
}
html.theme-dark .counterTitle-DPgs-R4s{
	color:var(--10B);
}
.tablesWrapper-DPgs-R4s{
	display:flex;
	justify-content:space-between;
	flex-wrap:wrap;
	border-top:1px solid;
	border-top-color:#f0f3fa;
	margin-bottom:40px
}
html.theme-dark .tablesWrapper-DPgs-R4s{
	border-top-color:#2a2e39
}
.tablesWrapper-DPgs-R4s table{
	width:100%
}
@media screen and (max-width:767px){
	.tablesWrapper-DPgs-R4s{
		border-top:none;
		margin-bottom:26px;
		margin-top:-4px
}
}
.summary-DPgs-R4s{
	order:1;
	flex-grow:2;
	width:100%;
	height:100%
}
.summary-DPgs-R4s .speedometerSignal-DPgs-R4s{
	margin:32px 0 10px;
	font-size:30px;
}
.page-wide .summary-DPgs-R4s{
	order:2;
	width:auto
}
.page-wide .speedometerWrapper-DPgs-R4s{
	min-width:auto
}
.popupClass-DPgs-R4s .summary-DPgs-R4s{
	order:1;
	flex-grow:2;
	width:100%
}
.tableWithAction-DPgs-R4s{
	flex-grow:0;
	flex-basis:calc(50%-20px)
}
.tableWithAction-DPgs-R4s tr td:last-child,.tableWithAction-DPgs-R4s tr th:last-child{
	text-align:left;
	width:60px
}
@media screen and (max-width:1019px){
	.tableWithAction-DPgs-R4s{
		flex:auto
}
}
@media screen and (max-width:767px){
	.tableWithAction-DPgs-R4s{
		margin:5px 0 14px
}
}
.maTable-DPgs-R4s tr:nth-child(2n){
	border-bottom:none
}
.maTable-DPgs-R4s tr:nth-last-child(-n+3){
	border-bottom:1px solid;
	border-bottom-color:#f0f3fa
}
html.theme-dark .maTable-DPgs-R4s tr:nth-last-child(-n+3){
	border-bottom-color:#2a2e39
}
.maTable-DPgs-R4s tr:last-child{
	border-bottom:none
}
@media screen and (max-width:500px){
	.speedometerWrapper-DPgs-R4s{
		min-width:0
}
	.summary-DPgs-R4s .speedometerSignal-DPgs-R4s{
		margin:25px 0 10px;
		font-size:24px
}
}
@media screen and (max-width:980px){
	.tablesWrapper-DPgs-R4s table{
		width:100%
}
	.speedometersContainer-DPgs-R4s{
		margin-left:0;
		margin-right:0
}
}
.techDialog-DPgs-R4s.techDialog-DPgs-R4s{
	max-width:980px;
	height:80%
}
.techDialog-DPgs-R4s.techDialog-DPgs-R4s .dialogSymbol-DPgs-R4s{
	font-size:22px;
	margin-bottom:20px
}
@media screen and (min-width:1530px){
	.techDialog-DPgs-R4s.techDialog-DPgs-R4s{
		max-width:1200px
}
	.techDialog-DPgs-R4s.techDialog-DPgs-R4s .summary-DPgs-R4s{
		order:2;
		width:auto
}
	.techDialog-DPgs-R4s.techDialog-DPgs-R4s .speedometerWrapper-DPgs-R4s{
		min-width:auto
}
}
.widget-technical-analysis__container{
	display:flex;
	flex-direction:column;
	width:100%;
	height:100%;
	overflow:auto;
	justify-content:center
}
.widget-technical-analysis a{
	color:#2962ff;
	transition:color .35s ease
}
html.theme-dark .widget-technical-analysis a{
	color:var(--HB);
	font-family:SofiaPro-Bold,sans-serif;
	font-size:24px;
	font-weight:700;
}
.widget-technical-analysis a:visited{
	color:var(--HB);
}
html.theme-dark .widget-technical-analysis a:visited{
	color:var(--HB);
}
@media (any-hover:hover),(min--moz-device-pixel-ratio:0){
	.widget-technical-analysis a:hover{
		color:var(--00B);
		fill:var(--00B);
		transition-duration:60ms
}
}
@media (any-hover:hover),(min--moz-device-pixel-ratio:0){
	html.theme-dark .widget-technical-analysis a:hover{
		fill:var(--00B);
		color:var(--00B);
}
}
.widget-technical-analysis a:focus{
	outline:auto
}
.widget-technical-analysis a:focus:not(:-moz-focusring){
	outline:none
}
.widget-technical-analysis a:-moz-focusring{
	outline:auto
}
.widget-technical-analysis a:active{
	fill:var(--00B);
	color:var(--00B);
	transition-duration:60ms
}
html.theme-dark .widget-technical-analysis a:active{
	fill:var(--00B);
	color:var(--00B);
}
.compactMargin-1mNRKgwm{
	margin-bottom:20px
}
.tabsWrap-1mNRKgwm{
	margin-bottom:20px;
	width:100%;
	--button-tabs-horizontal-scroll-padding:16px
}
.tv-embed-widget-wrapper{
	width:0;
	min-width:100%;
	max-width:100%;
	height:100%;
	background:transparent;
	font-family:SofiaPro-Bold,sans-serif;
	color:var(--10B);
}
.tv-embed-widget-wrapper__header{
	line-height:34px;
	font-size:13px;
	text-align:center
}
.tv-embed-widget-wrapper__header svg{
	vertical-align:text-top;
	margin-right:5px;
	width:26px;
	height:15px
}
.tv-embed-widget-wrapper__logo-link,.tv-embed-widget-wrapper__logo-link:visited{
	color:#2962ff
}
.tv-embed-widget-wrapper__body{
	position:relative;
	height:100%;
	background:#fff;
	border:1px solid #e0e3eb;
	box-sizing:border-box;
	border-radius:3px;
	overflow:hidden
}
html.theme-dark .tv-embed-widget-wrapper__body{
	background-color:var(--80B) !important;
	border:none;
}
.tv-embed-widget-wrapper__body--overflow_auto{
	overflow:auto
}
html.is-transparent .tv-embed-widget-wrapper__body{
	background:transparent
}
html.is-transparent .tv-embed-widget-wrapper__body:not(.tv-embed-widget-wrapper__body--border-on-transparent){
	border-width:0
}
.label-39Xi8p6T{
	display:flex;
	position:absolute;
	align-items:center;
	justify-content:flex-start;
	z-index:900;
	color:#fff;
	overflow:hidden;
	transition:background .3s cubic-bezier(.4,.01,.22,1) 0s;
	min-width:24px;
	height:24px;
	border-radius:12px
}
.label-39Xi8p6T:not(a){
	cursor:default
}
.label-39Xi8p6T.start-39Xi8p6T{
	left:8px;
	box-shadow:1px 0 3px 0 rgba(0,0,0,.16)
}
.label-39Xi8p6T.end-39Xi8p6T{
	right:8px;
	box-shadow:-1px 0 3px 0 rgba(0,0,0,.16)
}
.label-39Xi8p6T.snap-39Xi8p6T.start-39Xi8p6T{
	left:0;
	border-radius:0 12px 12px 0
}
.label-39Xi8p6T.snap-39Xi8p6T.end-39Xi8p6T{
	right:0;
	top:0;
	border-radius:12px 0 0 12px;
}
.label-39Xi8p6T.large-39Xi8p6T{
	min-width:32px;
	height:32px;
	border-radius:16px
}
.label-39Xi8p6T.large-39Xi8p6T.snap-39Xi8p6T.start-39Xi8p6T{
	border-radius:0 16px 16px 0
}
.label-39Xi8p6T.large-39Xi8p6T.snap-39Xi8p6T.end-39Xi8p6T{
	border-radius:16px 0 0 16px
}
.label-39Xi8p6T.top-39Xi8p6T{
	top:8px
}
.label-39Xi8p6T.bottom-39Xi8p6T{
	bottom:8px
}
.label-39Xi8p6T.chartBottom-39Xi8p6T{
	bottom:30px
}
.label-39Xi8p6T .textWrap-39Xi8p6T{
	display:inline-block;
	padding:0;
	max-width:0;
	white-space:nowrap;
	transition:max-width .6s cubic-bezier(.4,.01,.22,1) 0s
}
.label-39Xi8p6T .text-39Xi8p6T{
	padding-left:1px;
	padding-right:8px
}
@media (any-hover:hover),(min--moz-device-pixel-ratio:0){
	.label-39Xi8p6T:hover .textWrap-39Xi8p6T{
		max-width:118px
}
}
.label-39Xi8p6T:focus{
	outline:auto;
	outline-width:2px;
	outline-color:#2962ff;
	outline-offset:-2px
}
/* TradingView CSS */
/* Chart */
html.theme-dark html, body {
    background-color: var(--80B);
}
html.theme-dark .chart-page {
    background: var(--80B);
    border-radius: 3px;
    padding: 5px;
}
html.theme-dark body, html.theme-dark html {
    color: var(--10B);
}
html.theme-dark .chart-page .chart-container {
    background-color: var(--80B);
    border: none;
}
html.theme-dark .group-wWM3zP_M- {
    background-color: var(--70B);
}
html.theme-dark .button-13wlLwhJ- .arrow-2pXEy7ej- {
    color: var(--10B);
}
html.theme-dark .arrowGap-gjAe6jEn- {
    fill: var(--70B);
}
html.feature-no-touch.theme-dark .button-13wlLwhJ- .arrow-2pXEy7ej-:active, html.feature-no-touch.theme-dark .button-13wlLwhJ- .arrow-2pXEy7ej-:hover, html.feature-touch.theme-dark .button-13wlLwhJ- .arrow-2pXEy7ej-:active, html.theme-dark .button-13wlLwhJ- .arrow-2pXEy7ej-.hovered-FUo4RNOC- {
    color: var(--HB);
}
html.theme-dark .subGroup-1JpgB9zD->:not(:first-child):before {
    background-color: var(--80B);
}
html.theme-dark .button-13wlLwhJ-.isOpened-1939ai3F- {
    background-color: var(--60B);
}
html.theme-dark .button-2ioYhFEY- {
    color: var(--10B);
}
html.theme-dark .button-2ioYhFEY-.isInteractive-20uLObIc- {
    color: var(--10B);
}
html.theme-dark .button-13wlLwhJ- {
    color: var(--10B);
}
html.theme-dark .group-2JyOhh7Z- {
    background-color: var(--70B);
}
html.theme-dark .button-263WXsg-- {
    color: var(--10B);
}
html.theme-dark .button-263WXsg-- .icon-1Y-3MM9F- {
    color: var(--10B);
}
html.theme-dark .chart-controls-bar {
    background-color: var(--70B);
}
html.theme-dark .chart-controls-bar-buttons a {
    color: var(--10B);
}
.chart-controls-bar-buttons a.active, .feature-no-touch .chart-controls-bar-buttons a.active:hover {
    color: var(--10B) !important;
}
html.feature-no-touch.theme-dark .chart-controls-bar-buttons a:not(.disabled):hover {
    color: var(--10B) ;
    background-color: var(--HB) ;
}
html.theme-dark .inner-1xuW-gY4- {
    background-color: var(--80B);
}
html.feature-no-touch.theme-dark .button-263WXsg-- .icon-1Y-3MM9F-:active, html.feature-no-touch.theme-dark .button-263WXsg-- .icon-1Y-3MM9F-:hover, html.feature-touch.theme-dark .button-263WXsg-- .icon-1Y-3MM9F-:active, html.theme-dark .button-263WXsg-- .icon-1Y-3MM9F-.hovered--MYZioUu- {
    color: var(--HB);
}
html.feature-no-touch.theme-dark .button-13wlLwhJ-:active, html.feature-no-touch.theme-dark .button-13wlLwhJ-:hover, html.feature-touch.theme-dark .button-13wlLwhJ-:active, html.theme-dark .button-13wlLwhJ-.hovered-FUo4RNOC- {
    color: var(--HB);
}
html.feature-no-touch.theme-dark .button-2ioYhFEY-.isInteractive-20uLObIc-:active, html.feature-no-touch.theme-dark .button-2ioYhFEY-.isInteractive-20uLObIc-:hover, html.feature-touch.theme-dark .button-2ioYhFEY-.isInteractive-20uLObIc-:active, html.theme-dark .button-2ioYhFEY-.isInteractive-20uLObIc-.hovered-3perbaxJ- {
    color: var(--HB);
}
html.theme-dark .button-2ioYhFEY-.isInteractive-20uLObIc-.isOpened-p-Ume5l9- {
    background-color: var(--60B);
}
html.theme-dark .scrollBot-2HHpZNuf-, html.theme-dark .scrollTop-1eXi8ltS- {
    color: var(--90B);
    background-color: var(--HB);
}
html.theme-dark .container-3_8ayT2Q- .background-Q1Fcmxly- {
    stroke: none;
    fill: var(--60B);
}
html.feature-no-touch.theme-dark .container-3_8ayT2Q-:hover .background-Q1Fcmxly- {
    stroke: none;
    fill: var(--HB);
}
.container-3_8ayT2Q- .arrow-WcYWFXUn-, html.theme-dark .container-3_8ayT2Q- .arrow-WcYWFXUn- {
    stroke: var(--10B);
}
html.feature-no-touch.theme-dark .container-3_8ayT2Q-:hover .arrow-WcYWFXUn- {
    stroke: var(--10B);
}
html.theme-dark .layout__area--left {
    height: 455px !important;
}
.arrow-1cFKS5Ok- .arrowIcon-2wA7q8om- svg {
    fill: var(--10B);
}
.feature-no-touch .control-1TyEfSIx-:hover .arrow-1cFKS5Ok-:hover svg, .feature-no-touch .feature-touch .control-1TyEfSIx- .arrow-1cFKS5Ok-:hover svg, .feature-no-touch .isOpened-22vLOY9o- .control-1TyEfSIx- .arrow-1cFKS5Ok-:hover svg {
    fill: var(--HB);
    `);
    });
})();
