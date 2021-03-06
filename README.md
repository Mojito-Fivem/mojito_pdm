# mojito_pdm

React / Typescript Catalogue for PDM, complete with test driving and purchasing

![Light Theme](https://i.imgur.com/j0z9Z4H.png)
![Colour Picker](https://user-images.githubusercontent.com/66041893/146770988-a894b35f-a445-4e4c-b335-0a1a83685e85.png)


<p align="center">
	<a href="https://imgur.com/a/GozMbRX"> Imgur Album </a>
</p>

## Features
- High Performance Material UI
- Filter vehicles by category
- Pre-configured vehicles and prices
- Test Driving with configurable locations and timer
- Buy vehicles from the catalogue
- Finance vehicles
- View Outstanding Balances neatly organised in a menu
- Choose custom RGB colours for your vehicles

## Instalation
Download the latest version from the releases. Note that the master branch is not considered the most stable branch and you should not build from master unless you know what you're doing.

If you have buying and finance enabled you need to add the following to your database and install the [cron](https://github.com/esx-framework/cron) dependency
```sql
CREATE TABLE `vehicle_finance` (
    `id` INT(11) NOT NULL AUTO_INCREMENT,
    `plate` VARCHAR(10) NOT NULL COLLATE 'utf8mb4_general_ci',
    `citizenid` VARCHAR(50) NULL DEFAULT NULL COLLATE 'utf8mb4_general_ci',
    `model` VARCHAR(50) NULL DEFAULT NULL COLLATE 'utf8mb4_general_ci',
    `interest_rate` INT(11) NULL DEFAULT NULL,
    `outstanding_bal` INT(11) NULL DEFAULT NULL,
    `warning` TINYINT(4) NULL DEFAULT '0',
    PRIMARY KEY (`id`) USING BTREE,
    INDEX `citizenid` (`citizenid`) USING BTREE,
    INDEX `plate` (`plate`) USING BTREE
) COLLATE='utf8_general_ci' ENGINE=InnoDB AUTO_INCREMENT=1;

```

## Config

```js
{
  "pdmlocation": {"x": -56.54, "y": -1096.18, "z": 26.42},                            // Location to teleport the player back to
  "testdrivespawn": {"x": -16.84, "y":  -1105.11, "z": 26.36, "h": 158.76},           // Location to spawn the car for test drives
  "buylocation": {"x": -16.84, "y":  -1105.11, "z": 26.36, "h": 158.76},	      // Location to spawn the car when it is purchased
  "temporary": {
    "enabled": true,                                                                  // Enable time limit on test drives
    "time": 120                                                                       // Time (in seconds) of the test drive
  },
  "canbuy": true,								      // Set to false to disable buying vehicles
  "colours": true,                                                                    // Set to false to disable custom RGB colours      
  "limit": {                                              
    "enabled": true,                                                                  // Set to true to restrict usage when car dealers are online                                  
    "jobname": "cardealer",                                                           // Name of car dealer job
    "count": 2                                                                        // Maximum amount of car dealers that can be online before restrictions
  },
  "finance": {
    "installment_percent": 10,                                                        // Percentage cost of finance installments
    "runs_on": 1,                                                                     // The day of the week the installments are taken 1 = monday
    "runs_at": "18:30"                                                                // The time of day the installments are taken in 24h format
  },
  "qbtarget": true                                                                    // Enable qb-target by default  
}
```

By default `mojito_pdm` comes with some preconfigured vehicles from the base build (DLC content is not included). To add more cars simply add to the `cars.json` file, this no longer requires a re-build and changes will be seen after restarting the resource.

## Usage

By default, the resource is configured with qb-target however if you wish to disable this and do it your own way you can do the following: 

To open the catalogue trigger the event `mojito_pdm:client:open`
To open the propmt to check finance trigger the event `mojito_pdm:client:check_finance`


## Building

Builds are automatically generated when a tagged release is pushed, to build manually from the master branch you can use the following:

### Yarn:

To build the UI:
`cd ui` -> `yarn` -> `yarn build`

To build the script:
`cd resources` -> `yarn` -> `yarn build`

### NPM:

To build the UI:

`cd ui` -> `npm i` -> `npm run build`

To build the script:

`cd resources` -> `npm i` -> `npm run build`

## Developing

Issues and pull requests are welcomed.

This project is using [Project Error's React Boilerplate](https://github.com/project-error/fivem-react-boilerplate-lua) which comes with useful utilities, use `yarn start` to start the dev server or `yarn start:game` to open the dev server and build at the same time.

## Credits

- Images and Brand Logos taken from [GTA Fandom Wiki](https://gta.fandom.com/wiki/) under CC-BY-SA license
- Build and Release script taken from [fivem-appearance](https://github.com/pedr0fontoura/fivem-appearance) under MIT license
- Github Actions workflow was created by [Taso](https://github.com/TasoOneAsia) for [txAdmin](https://github.com/tabarra/txAdmin) under MIT license


<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
