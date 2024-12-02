# 1、预言机攻击案例
	PROJECT NAME：EGD Finance 
	CA：0x34Bd6Dba456Bc31c2b3393e499fa10bED32a9370 
	EVM:BSC
  	HASH: https://phalcon.blocksec.com/tx/bsc/0x50da0b1b6e34bce59769157df769eb45fa11efc7d0e292900d6b0a86ae66a2b3
	DETAIL:
	https://github.com/SunWeb3Sec/DeFiHackLabs/tree/main/academy/onchain_debug/03_write_your_own_poc/
	step：
	1、攻击者发现EGD Finance合约的质押奖励的token数量计算使用了代币池的实时价格漏洞,使用者领取的 Staking Reward 数量，
 	取决于奖励因子 quota（代表用户 Staking 多少代币、Staking 多久时间）乘上 getEGDPrice () 合约给出的 EGD Staking Reward 
  	会按照目前的 EGD Token 市价给予更多或更少的 Token 数量，当 EGD Token 价格越高，则给予的 EGD Token 数量越少，
   	当 EGD Token 价格越低，则给予的 EGD Token 数量越多
	rew+= quota * 1e18 / getEGDPrice()  
 	
 	2、攻击者在第二层闪电贷，向 EGD/USDT Pair 借出 USDT；在攻击者还款之前，getEGDPrice () 获取到的价格信息就会是不正确的。
  
  	3、攻击者通过闪电贷，抽走价格预言机的流动性，使 ClaimReward () 获取到不正确的价格参考，进而使攻击者可以领取到异常大量的 EGD Token。
	攻击者利用漏洞取得大量 EGD Token 后，将 EGD Token 通过 Pancakeswap 换回 USDT，获利了结。

![](https://github.com/cxl-xuaner/DefiHackLab_temp-example/blob/main/pic/claimALLRewardfunc.png)
 
![](https://github.com/cxl-xuaner/DefiHackLab_temp-example/blob/main/pic/getPrice.png)

![](https://github.com/cxl-xuaner/DefiHackLab_temp-example/blob/main/pic/priceChangeExample.png)
 
	
	
	
