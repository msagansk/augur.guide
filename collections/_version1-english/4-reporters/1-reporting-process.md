---
title: Reporting Process
---

# Reporters: Reporting Process

Ok, let’s blow up the reporting process box from ["The Life of a Market"]({{ "/" | absolute_url }}/{{page.collection}}/1-getting-started/the-life-of-a-market.html) page into its detailed sub-steps and go over them:

<div class="center">
{% capture image_url %}
  /assets/images/{{page.collection}}/Reporting Flowchart.svg
{% endcapture %}
{% include image.html url=image_url description="Figure 1. Reporting Flowchart" %}
</div>

1. [**Designated Reporting**]({{ "/" | absolute_url }}/{{page.collection}}/7-glossary.html#Designated_Reporting_Phase) - This is the first step of the reporting phase and is triggered by the market [end time]({{ "/" | absolute_url }}/{{page.collection}}/7-glossary.html#End_Time) occurring, which was originally set by the market creator when the market was created. The market creator picked an address to be the [designated reporter]({{ "/" | absolute_url }}/{{page.collection}}/7-glossary.html#Designated_Reporter), which is usually the market creator itself. This designated reporter now has 3 days to perform the [initial report]({{ "/" | absolute_url }}/{{page.collection}}/7-glossary.html#Initial_Report), which is the first [tentative outcome]({{ "/" | absolute_url }}/{{page.collection}}/7-glossary.html#Tentative_Outcome) for the market. The designated reporter has to post a [bond]({{ "/" | absolute_url }}/{{page.collection}}/7-glossary.html#Designated_Reporter_Stake) (in REP) to incentivise other reporters to make sure the outcome selected is the correct answer. The designated reporter does not get to unilaterally decide how the market resolves, the rest of the reporter community has to generally agree. This decentralized resolution process is one of the main strengths of Augur, but it can also cause delays in resolution.

2. **Designated Reporter Reported?** - Did the designated reporter perform the initial report in the required 3 day window? It is possible that the designated reporter forgot to do so (or neglected to do so for some other reason), which means the market will go into [Open Reporting]({{ "/" | absolute_url }}/{{page.collection}}/7-glossary.html#Open_Reporting_Phase). If the initial report was performed, the market will wait for the next fee window to give other reporters some time to analyze the market and potentially dispute an incorrect tentative outcome.

3. **Open Reporting** - Anyone can now perform the initial report to potentially claim the [“no-show” REP bond]({{ "/" | absolute_url }}/{{page.collection}}/7-glossary.html#No-Show_Bond) the market creator posted. The bond will be rewarded if the initially reported outcome ends up becoming the finalized outcome. This is essentially “free money”, so competition to do open reporting is fierce.

4. **Waiting for Next [Fee Window]({{ "/" | absolute_url }}/{{page.collection}}/7-glossary.html#Fee_Window)** - Augur groups all markets into the same 7 day time period/fee window. So, whenever an initial report or dispute occurs, there is a delay before another dispute can occur. This delay is deliberate, it allows for reporters to have a reliable schedule to analyze and discuss questionable markets, gather support for a particular outcome, and acquire enough REP from cold storage if necessary. The start of a fee window is currently set to be every Thursday at 00:00:00 UTC. 

5. [**Dispute Round**]({{ "/" | absolute_url }}/{{page.collection}}/7-glossary.html#Dispute_Round) - This is the same thing as the fee window. It has two names because reporting fees from markets are collected and dispersed in 7 day chunks based on reporting activity during that same time period. This is the time for reporters to dispute a tentative outcome if they believe it is not the correct answer. Different markets can be in different dispute round numbers, depending on how many times a market has been disputed. Successive dispute rounds escalate the amount of required REP to dispute the tentative outcome until it is no longer disputed or the [fork threshold]({{ "/" | absolute_url }}/{{page.collection}}/7-glossary.html#Fork_Threshold) is reached. 

6. **Tentative Outcome Disputed?** - A market has to have one of its (non-tentative) outcomes REP bonds filled in order to successfully dispute the current tentative outcome. The amount of REP required to dispute scales depending on how many outcomes are in dispute. For the most typical case where only two outcomes are being disputed, the required REP bond doubles every round. This allows for a 50% return on investment for the reporters who staked on the final outcome, while the reporters who staked on the incorrect outcome(s) lose their bond. If the required REP bond is not filled, the market is no longer in dispute, so it moves to the resolved state and the reporting phase is over.

7. **Dispute Bond Above Fork Threshold?** - The dispute bond has been filled for one of the (non-tentative) outcomes so a check is performed. If the required bond was at least 2.5% of the total supply of REP, the market triggers a fork. If the required bond was not that high, the disputed outcome becomes the new tentative outcome and the market waits for the next fee window to begin (i.e. loop back to step 4).

8. **Fork** - Getting an Augur market to this state should be a rare occurrence, because there are cryptoeconomic security guarantees that make it very costly for an attack to do this maliciously. Forks are a very disruptive process that can take a long time to resolve (up to 60 days). While an Augur market is in this state, no new markets can be created and the reporting process for all other markets pauses. All REP holders who want to use Augur then have to decide what the correct answer is for the forking market. New [universes]({{ "/" | absolute_url }}/{{page.collection}}/7-glossary.html#Universe) are created for each potential outcome, spawned from the current [genesis universe]({{ "/" | absolute_url }}/{{page.collection}}/7-glossary.html#Genesis_Universe) where the forking market originated from. Deciding which outcome is correct means staking REP on that outcome, which means moving REP into that universe. That universe is separate from all the other universes (they don’t share markets, trading fees, etc). The answer that receives the most REP wins the fork and is the winning outcome, and all of the pre-existing markets from the genesis universe move into the winning one. Market creators and traders also have to decide on which universe they want to participate in as well. It is assumed that all regular users will want to interact with the truthful one. A forked market can no longer be disputed and is considered finalized once the fork is complete. A more thorough technical explanation of the forking process is explaining on the [Forks]({{ "/" | absolute_url }}/{{page.collection}}/4-reporters/3-forks.html) page.