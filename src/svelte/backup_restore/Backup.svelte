<script> 
    import { getContext } from 'svelte';

    //Stores
    import { needsBackup, SettingsStore } from '../../js/stores/stores.js';

    //Components
	import { Components }  from '../Router.svelte'
    const { Button } = Components;
    
    //Images
    import squares_bg from '../../img/backgrounds/squares_bg.png';
    import arrowRight from '../../img/menu_icons/icon_arrow-right.svg';
    import warningIcon from '../../img/menu_icons/icon_warning.svg'
    import iconClose from '../../img/menu_icons/icon_close.svg'


	//Context
    const { switchPage } = getContext('app_functions');


    const dismissWarning = () => {SettingsStore.dismissWarning()}

</script>

<style>
.backup{
	display: flex;
	flex-direction: column;
}

.hero-rec{
    display: flex;
    flex-direction: column;
	box-sizing: border-box;
	min-height: 310px;
	border-radius: 4px;
	margin-bottom: 18px;
    padding: 40px;
    background-size: cover;
    background-repeat: no-repeat;
}

.buttons{
    display: flex;
    flex-direction: row;
    align-items: flex-end;
    flex-grow: 1;
    margin-top: 4rem;
}

.subtext{
    max-width: 601px;
    line-height: 1.4;
}

.backup-warning{
    align-items: center;
    margin-top: 1rem;
}

.warning-icon{
    width: 20px;
    margin-right: 10px;
    min-width: 20px;
}


</style>

<div class="backup text-primary">
	<div class="hero-rec" style="background-image: url({squares_bg});">
        <h2 class="heading">
            Backing Up Your Lamden Wallet is Very Important
        </h2>
        <div class="subtext text-body1 text-primary-dark">
            All of the information for your Accounts is stored in this browser. 
            We highly recommend creating a KeyStore file so that you can recover 
            your accounts if anythign happens to this computer.
        </div>
        <div class="buttons">
        	<Button
                id={'backup-btn'} 
                classes={'button__transparent button__blue'}
				name="Backup Wallet"
                margin={'0 49px 0 0'}
		 		click={() => switchPage('BackupMain')} 
				icon={arrowRight}
                iconPosition='after'/>
        </div>
        {#if $needsBackup}
            <div class="flex-row backup-warning">
                <div class="warning-icon">{@html warningIcon}</div>
                <div class="warning-text text-body4">
                    You have added Accounts since your last backup so it is HIGHLY recommended that you create another backup.
                </div>
                <Button
                    id={'dismiss-btn'} 
                    classes={'button__icon'}
                    height="unset"
                    padding={'0'}
                    click={dismissWarning} 
                    icon={iconClose}
                    iconInvert={true}
                    iconPosition='after'/>
            </div>
        {/if}
	</div>
</div>
