yam - Yet Another Miner by yvg1900 - optimized miner for cryptocurrency mining

*** If you want to stay informed on updates, follow @yvg1900 on Twitter.

DISCLAIMER

The software comes as it is, without warranty of any kind. It is solely your decision to use it or not. 
Use at your own risk, the creator can not be held liable for damage to your system.
If you are in doubt - don't use it.

Please read this file carefully. To achieve better performance consider using fine tuning feature as described in finetuning-<coin>.txt.
You can check if your miner is actually connected to your account on the pool site in Workers area or other means supported by pool.

Miner periodically mines for miner developers to support further performance, functionality and compatibility enhancements.
Explanation of how and when it happens can be found below in "Mining for developers" section.

1. How yam is different from other miners

This miner created completely from scratch, including mining framework, mining algorithms, connection handling, etc.

Comparing to other miners, yam includes following changes and improvements:
  - Support for ProtoShares, MemoryCoin, MaxCoin, GroestlCoin, DiamondCoin, DvoraKoin, MyriadCoin,
    ByteCoin, QuazarCoin, FantomCoin and Monero mining
  - Much higher performance
  - Configuration file support
  - Completely different connection handling that reduces connection latency and minimizes amount of wasted CPU time, while
    minimizing unnecessary CPU load
  - Server pinging to fix NAT connectivity and some other networking and reconnection problems
  - Dynamic connection timeout system for early detection of connectivity problems
  - Multiple pool connections for mining on secondary pool when primary pool is down
  - SOCKS4A Proxy support (compatible with Tor)
  - SOCKS5 Proxy support
  - Compatibility check mode for easier miner selection in automated deployment environment
  - Possibility to go above 512M per thread for PTS mining
  - Algorithm fine tuning feature
  - Fine-grained CPU pinning/affinity control

2. Which build to use

* Know your machine. Carefully check capabilities of your CPU in order to determine its capabilities. You will need to know:
  - Your operating system
  - Model and microarchitecture of your CPU
  - Is it physical or virtualized
  - Does it support SSE, AVX and other modern instruction sets, and if yes - which versions
  - Are AES-NI instructions available
  - How many physical cores your CPU has
  - Does your CPU support HyperThreading or not
  - How many CPUs your machine has in case you are on multi-CPU machine
  - How much RAM do you have

Build are located in the folders, each folder per build. Folders named as

yam-yvg1900-<miner version>-<operating system name>-<instruction set>

For example, for 64-bit Linux running on Haswell CPU with, take linux64-haswell build. 
More builds will become available as soon as there is more demand and sufficient donations.

Feel free to try different builds, but be aware that some may crash due to lack of support for specific instructions on your machine.

Note that consistency of builds can be verified by wallet sowftware using "File/Verify Message..." command. You can find MD5 checksums
in yam-md5sums.txt file and appropriate signatures in yam-md5sums-signature.txt file. Note that yam-md5sums.txt uses Linux style
line breaks, so Windows users may see incorrect formatting when using Windows Notepad program to view it. Line breaks shall work
correctly after copy-paste file content into "Verify Message" window.

2.1. Some guidelines on selecting build

bdver1:
  AMD Opteron� 6200 Series processors
  AMD Opteron� 4200 Series processors

bdver2:
  AMD Opteron� 6300 Series processors
  AMD Opteron� 4300 Series processors

btver2:
  AMD Opteron� X1100 series Processor
  AMD Opteron� X2100 series APU

2.2. Instruction set requirements for GroestlCoin and DiamondCoin mining

Note that GRS/DMD/DVK/MYR/BCN/QCN/FCN/XMR mining for AVX and AVX2 instruction sets require AES-NI support. 
AES-NI support required by GRS/DMD/DVK/MYR/BCN/QCN/FCN/XMR algorithm implementations 
in following builds:

  sandy-bridge
  ivy-bridge
  haswell
  bdver1
  bdver2
  btver2

If your CPU supports AVX, but does not support AES-NI, consider using other builds.

Note that non-AES-NI builds for GRS/DMD/DVK/MYR/BCN/QCN/FCN/XMR are definitely suboptimal. If you really want them optimized
and wish to offer reasonable bounty, please contact developers to discuss details.

3. Running and terminating the miner

You can run it from command prompt, either manually or create a batch file (.bat on Windows) or a shell script (on non-Windows).

To stop miner, kill it by pressing Ctrl+C in the shell window where it runs, or kill it using Task Manager or kill command.

4. Command line arguments

Command-line only options:
  --help                This message.
  -c [ --config ] arg   Name of configuration file. Multiple configuration files allowed.
  --compat-check arg    Exit right after compatibility checks with provided return code.

Command-line and configuration file options:
  -t [ --threads ] arg       The number of threads for mining (default is to
                             autodetect), when t<=0 use autodetect+t threads.
  -M [ --mine ] arg          Mining target in YAM URI format (protocol, worker
                             name, password, pool address, pool ports, coin
                             type, mining parameters). Multiple mining targets
                             allowed.
  -P [ --mining-params ] arg Mining parameters in parameter list format
                             (coin:param1=value1&param2=value2&param3=value3.
                             Multiple parameter groups allowed.
  -W [ --worker-params ] arg Worker parameters in parameter list format
                             (worker_index:param1=value1&param2=value2&param3=value3. 
                             Multiple parameter groups allowed.
  --compact-stats arg        Enable compact statistics output (uses less screen
                             space).
  --print-timestamps arg     Enable printing timestamps for every output line.
  --proxy arg                Proxy server to use in format
                             type://user:password@host:port (check
                             documentation for supported proxy types and usage
                             details).

Easiest way to run miner is to modify example config file provided with the miner and run

yam --config yam.cfg

4.1. Mining target format

The best explanation is example.

For ProtoShares:
Mining target for ypool: xpt2h://yvg1900.defpts:x@mining.ypool.net:10034:8080:8081:8082:8083:8084:8085:8086:8087/pts
Mining target for ptspool: xpt2://PsPhfpU91JWTgt5A4AS4eVyuZJQQXAhrjW:x@112.124.13.238:28988/pts
Mining target for beeeeer: xram4://Pm9LE8UxTo5TQZdfH2RqcbNfCBiK1KWCtV@ptsmine.beeeeer.org:1337/pts
Mining target for 1gh: xpt2h://Pm9LE8UxTo5TQZdfH2RqcbNfCBiK1KWCtV:x@ptspool.1gh.com:18120:18121:18122:18123/pts
Mining target for upcpu: xpt2h://Pm9LE8UxTo5TQZdfH2RqcbNfCBiK1KWCtV:x@xptspool.upcpu.com:8080:8081:8082:8083:8084:8085:8086:8087/pts

For MemoryCoin:
Mining target for mmcpool: getwork://MTb1JHjoJCSJBjTLUgqeyJ1nXxYxBRJEUX@work.mmcpool.com:80:8880:8881:8882:8883/mmc
Mining target for 1gh: getwork://MTb1JHjoJCSJBjTLUgqeyJ1nXxYxBRJEUX@mmcpool.1gh.com:8080:8081:8082:8083/mmc
Mining target for dwarfpool: getwork://MTb1JHjoJCSJBjTLUgqeyJ1nXxYxBRJEUX@erebor.dwarfpool.com:8080:8081:8082:8083/mmc
                             getwork://MTb1JHjoJCSJBjTLUgqeyJ1nXxYxBRJEUX@moria.dwarfpool.com:8080:8081:8082:8083/mmc
Mining target for P2Pool based pools: stratum+tcp://MTb1JHjoJCSJBjTLUgqeyJ1nXxYxBRJEUX@<pool address>:8080/mmc

For MaxCoin:
Mining target for dwarfpool: stratum+tcp://mafx9Lig1LGZSj6Ti5gZE8Tj1TjWwGF6YL@moria.dwarfpool.com:3339/max
                             stratum+tcp://mafx9Lig1LGZSj6Ti5gZE8Tj1TjWwGF6YL@erebor.dwarfpool.com:3339/max
Mining target for 1gh: stratum+tcp://mafx9Lig1LGZSj6Ti5gZE8Tj1TjWwGF6YL@maxpool.1gh.com:17333/max
                       stratum+tcp://mafx9Lig1LGZSj6Ti5gZE8Tj1TjWwGF6YL@maxpool2.1gh.com:17333/max
Mining target for rocketpool: stratum+tcp://mafx9Lig1LGZSj6Ti5gZE8Tj1TjWwGF6YL@max.rocketpool.co.uk:3333:443/max
Mining target for maxcoinpool: stratum+tcp://yvg1900.max_1:x@eu.maxcoinpool.com:4000/max
                               stratum+tcp://yvg1900.max_1:x@us.maxcoinpool.com:4000/max
Mining target for maxcoin.co.nz: stratum+tcp://yvg1900.max_1:x@anz.mine.maxcoin.co.nz:3333/max
                                 stratum+tcp://yvg1900.max_1:x@us.mine.maxcoin.co.nz:3333/max
Mining target for hashfaster: stratum+tcp://yvg1900.max_1:x@stratum1.max.hashfaster.com:4004/max
                              stratum+tcp://yvg1900.max_1:x@stratum-east.max.hashfaster.com:4004/max
Mining target for other pools: stratum+tcp://yvg1900.max_1:x@stratum2.iwakuang.com:1234/max
                               stratum+tcp://yvg1900.max_1:x@max.coinedpool.com:3348:3349:3350/max
                               stratum+tcp://yvg1900.max_1:x@max.mining4all.eu:3332/max
                               stratum+tcp://yvg1900.max_1:x@maxus.nut2pools.com:6010/max
                               stratum+tcp://yvg1900.max_1:x@max.suprnova.cc:3333/max
                               stratum+tcp://yvg1900.max_1:x@ypool.net:9090/max

For GroestlCoin:
Mining target for dwarfpool: stratum+tcp://FnBbSE57cpCkEdu2eu38eNRVwkFLxMn4Lz@erebor.dwarfpool.com:3345/grs
                             stratum+tcp://FnBbSE57cpCkEdu2eu38eNRVwkFLxMn4Lz@moria.dwarfpool.com:3345/grs
Mining target for miningpoolhub: stratum+tcp://yvg1900.grs_1:x@us-east1.groestlcoin.miningpoolhub.com:20486/grs?noping&difficulty-multiplier=1.0
                                 stratum+tcp://yvg1900.grs_1:x@asia1.groestlcoin.miningpoolhub.com:20486/grs?noping&difficulty-multiplier=1.0
                                 stratum+tcp://yvg1900.grs_1:x@europe1.groestlcoin.miningpoolhub.com:20486/grs?noping&difficulty-multiplier=1.0
Mining target for other pools: stratum+tcp://yvg1900.grs_1:x@grs.cpu-pool.net:3650/grs
                               stratum+tcp://yvg1900.grs_1:x@grs.suprnova.cc:5544/grs
                               stratum+tcp://yvg1900.grs_1:x@cryptohunger.com:3333/grs
                               stratum+tcp://yvg1900.grs_1:x@mine1.coinmine.pl:3000/grs
                               stratum+tcp://FnBbSE57cpCkEdu2eu38eNRVwkFLxMn4Lz@groestlcoin.biz:3333/grs?noping

For DiamondCoin:
Mining target for various pools: stratum+tcp://yvg1900.dmd_1:x@dmdpool.digsys.bg:3333/dmd?noping
                                 stratum+tcp://dHyi2FUbd3ziLfBkugRjMyTDDd4mTLrtjp@groestlcoin.biz:3334/dmd?noping
                                 stratum+tcp://dHyi2FUbd3ziLfBkugRjMyTDDd4mTLrtjp@stratum.cryptofrenzy.eu:4444/dmd?noping
                                 stratum+tcp://yvg1900.dmd_1:x@mine3.dmd.nonce-pool.com:4030/dmd

For DvoraKoin: 
Mining target for various pools: stratum+tcp://DNzL1JEWhsPVMuxaaUTRrfsH9uHFFBbmDS@p2poolcoin.com:5353/dvk
                                 stratum+tcp://DNzL1JEWhsPVMuxaaUTRrfsH9uHFFBbmDS@ca.p2poolcoin.com:5353/dvk

For MyriadCoin: 
Mining target for miningpoolhub: stratum+tcp://yvg1900.myr_1:x@us-east1.myriadcoin-groestl.miningpoolhub.com:20479/myr?noping
                                 stratum+tcp://yvg1900.myr_1:x@us-east1.myriadcoin-groestl.miningpoolhub.com:20479/myr?noping

Mining target for various pools: stratum+tcp://yvg1900.myr_1:x@myrgrs.suprnova.cc:5678/myr

For ByteCoin: 
Mining target for various pools: stratum+tcp://2AcGMZmmNWTiLvAg5n7ywMCAxXTxysYGsi1xzba2ok4UPccWTLqRyKN7EnQYUpEWpqBw1c9EVZrqo2CUG8f8mbjG5NA9njF:x@bcn.extremepool.org:5555:7777:3333/bcn
                                 stratum+tcp://2AcGMZmmNWTiLvAg5n7ywMCAxXTxysYGsi1xzba2ok4UPccWTLqRyKN7EnQYUpEWpqBw1c9EVZrqo2CUG8f8mbjG5NA9njF:x@bcn.ext-pool.net:3101:3102/bcn
                                 minergate://yvg1900%40gmail.com:x@fcn-bcn.pool.minergate.com:5558/bcn?session-length=500
                                 minergate://yvg1900%40gmail.com:x@bcn.pool.minergate.com:5555/bcn?session-length=500

For QuazarCoin: 
Mining target for various pools: stratum+tcp://1V6wZP6aycYPbeafHxPcvaQfGs4M5kabHDQoTEsyCTT3HjccMyQbvEVNPoJuRc79XrPRYWESiAezyipWojpZ8bii3kczNgW:x@minin.gs:13333:15555:17777/qcn
                                 stratum+tcp://1V6wZP6aycYPbeafHxPcvaQfGs4M5kabHDQoTEsyCTT3HjccMyQbvEVNPoJuRc79XrPRYWESiAezyipWojpZ8bii3kczNgW:x@qcnpool.org:2222:3333/qcn
                                 stratum+tcp://1V6wZP6aycYPbeafHxPcvaQfGs4M5kabHDQoTEsyCTT3HjccMyQbvEVNPoJuRc79XrPRYWESiAezyipWojpZ8bii3kczNgW:x@qcn.extremepool.org:5555:7777/qcn
                                 stratum+tcp://1V6wZP6aycYPbeafHxPcvaQfGs4M5kabHDQoTEsyCTT3HjccMyQbvEVNPoJuRc79XrPRYWESiAezyipWojpZ8bii3kczNgW:x@qcn.hashinvest.ws:13333:15555/qcn
                                 stratum+tcp://1V6wZP6aycYPbeafHxPcvaQfGs4M5kabHDQoTEsyCTT3HjccMyQbvEVNPoJuRc79XrPRYWESiAezyipWojpZ8bii3kczNgW:x@qcn.ext-pool.net:3004:3005:3006/qcn
                                 stratum+tcp://1V6wZP6aycYPbeafHxPcvaQfGs4M5kabHDQoTEsyCTT3HjccMyQbvEVNPoJuRc79XrPRYWESiAezyipWojpZ8bii3kczNgW:x@qcn.cryptity.com:6666/qcn
                                 stratum+tcp://1V6wZP6aycYPbeafHxPcvaQfGs4M5kabHDQoTEsyCTT3HjccMyQbvEVNPoJuRc79XrPRYWESiAezyipWojpZ8bii3kczNgW:x@qcn.server.5limi.com:4001:4002:4003/qcn
                                 stratum+tcp://1V6wZP6aycYPbeafHxPcvaQfGs4M5kabHDQoTEsyCTT3HjccMyQbvEVNPoJuRc79XrPRYWESiAezyipWojpZ8bii3kczNgW:x@webcoin.me:5556:7776/qcn
                                 minergate://yvg1900%40gmail.com:x@fcn-qcn.pool.minergate.com:5560/qcn?session-length=500
                                 minergate://yvg1900%40gmail.com:x@qcn.pool.minergate.com:5557/qcn?session-length=500

For FantomCoin: 
Mining target for various pools: minergate://yvg1900%40gmail.com:x@fcn-mro.pool.minergate.com:5559/fcn?session-length=500
                                 minergate://yvg1900%40gmail.com:x@fcn-bcn.pool.minergate.com:5558/fcn?session-length=500
                                 minergate://yvg1900%40gmail.com:x@fcn-qcn.pool.minergate.com:5560/fcn?session-length=500

For Monero: 
Mining target for various pools: stratum+tcp://45w9aqVA6iVeMJ6jVHZPEyPqgVnBEAGhBBqGAW9ncXp44qbZy9vXkd2KpqYwcyVTQHF1kaSJm97GyceP3Y2dRMd7E9gyuZf:x@mine.moneropool.com:3336:3335:3334:3333/xmr
                                 stratum+tcp://45w9aqVA6iVeMJ6jVHZPEyPqgVnBEAGhBBqGAW9ncXp44qbZy9vXkd2KpqYwcyVTQHF1kaSJm97GyceP3Y2dRMd7E9gyuZf:x@mro.extremepool.org:5555:3333:7777/xmr
                                 stratum+tcp://45w9aqVA6iVeMJ6jVHZPEyPqgVnBEAGhBBqGAW9ncXp44qbZy9vXkd2KpqYwcyVTQHF1kaSJm97GyceP3Y2dRMd7E9gyuZf:x@kippo.eu:3003/xmr
                                 stratum+tcp://45w9aqVA6iVeMJ6jVHZPEyPqgVnBEAGhBBqGAW9ncXp44qbZy9vXkd2KpqYwcyVTQHF1kaSJm97GyceP3Y2dRMd7E9gyuZf:x@pool.minexmr.com:5555:7777:3333/xmr
                                 stratum+tcp://45w9aqVA6iVeMJ6jVHZPEyPqgVnBEAGhBBqGAW9ncXp44qbZy9vXkd2KpqYwcyVTQHF1kaSJm97GyceP3Y2dRMd7E9gyuZf:x@mine.moneropool.org:80/xmr
                                 stratum+tcp://45w9aqVA6iVeMJ6jVHZPEyPqgVnBEAGhBBqGAW9ncXp44qbZy9vXkd2KpqYwcyVTQHF1kaSJm97GyceP3Y2dRMd7E9gyuZf:x@monero.crypto-pool.fr:6666/xmr
                                 stratum+tcp://45w9aqVA6iVeMJ6jVHZPEyPqgVnBEAGhBBqGAW9ncXp44qbZy9vXkd2KpqYwcyVTQHF1kaSJm97GyceP3Y2dRMd7E9gyuZf:x@pool.cryptoescrow.eu:3333/xmr
                                 stratum+tcp://45w9aqVA6iVeMJ6jVHZPEyPqgVnBEAGhBBqGAW9ncXp44qbZy9vXkd2KpqYwcyVTQHF1kaSJm97GyceP3Y2dRMd7E9gyuZf:x@xmr.hashinvest.ws:5555:1111/xmr
                                 stratum+tcp://45w9aqVA6iVeMJ6jVHZPEyPqgVnBEAGhBBqGAW9ncXp44qbZy9vXkd2KpqYwcyVTQHF1kaSJm97GyceP3Y2dRMd7E9gyuZf:x@monero.farm:1337/xmr
                                 stratum+tcp://45w9aqVA6iVeMJ6jVHZPEyPqgVnBEAGhBBqGAW9ncXp44qbZy9vXkd2KpqYwcyVTQHF1kaSJm97GyceP3Y2dRMd7E9gyuZf:x@cryptonotepool.org.uk:5555/xmr
                                 stratum+tcp://45w9aqVA6iVeMJ6jVHZPEyPqgVnBEAGhBBqGAW9ncXp44qbZy9vXkd2KpqYwcyVTQHF1kaSJm97GyceP3Y2dRMd7E9gyuZf:x@monerominers.net:7777:7778/xmr
                                 stratum+tcp://45w9aqVA6iVeMJ6jVHZPEyPqgVnBEAGhBBqGAW9ncXp44qbZy9vXkd2KpqYwcyVTQHF1kaSJm97GyceP3Y2dRMd7E9gyuZf:x@webcoin.me:5555:7777/xmr
                                 stratum+tcp://45w9aqVA6iVeMJ6jVHZPEyPqgVnBEAGhBBqGAW9ncXp44qbZy9vXkd2KpqYwcyVTQHF1kaSJm97GyceP3Y2dRMd7E9gyuZf:x@xmr.coinmine.pl:5555:7777/xmr
                                 stratum+tcp://45w9aqVA6iVeMJ6jVHZPEyPqgVnBEAGhBBqGAW9ncXp44qbZy9vXkd2KpqYwcyVTQHF1kaSJm97GyceP3Y2dRMd7E9gyuZf:x@mro.poolto.be:3000:3001/xmr
                                 stratum+tcp://45w9aqVA6iVeMJ6jVHZPEyPqgVnBEAGhBBqGAW9ncXp44qbZy9vXkd2KpqYwcyVTQHF1kaSJm97GyceP3Y2dRMd7E9gyuZf:x@mine.moneropool.com.br:3333/xmr
                                 minergate://yvg1900%40gmail.com:x@fcn-mro.pool.minergate.com:5559/xmr?session-length=500
                                 minergate://yvg1900%40gmail.com:x@mro.pool.minergate.com:5556/xmr?session-length=500

More protocol support and pools to come.

Place mining targets in order of your preference. First target will be treated as primary mining target, and majority of the mining will be done with it.

4.2. Mining parameters format

Mining parameters are coin-specific.

For ProtoShares, allowed parameters are: 
  "av" (algorithm variation, 32 variations in total, 0 activates fine tuning feature)
  "m" (memory size per thread in megabytes)
  "donation-interval" (in mining rounds)

Mining parameters example for ProtoShares: pts:av=8&m=1024&donation-interval=50

For MemoryCoin, allowed parameters are: 
  "av" (algorithm variation, 6 variations in total, 0 activates fine tuning feature) [current version forces av=1 for non-AES-NI setups]
  "aesni" (activate AES-NI instructions support, "on" activates AES-NI, "off" deactivates AES-NI)
  "m" (memory size for mining in megabytes, minimum is 1024, shall be multiple of 1024)
  "donation-interval" (in mining rounds)

Mining parameters example for MemoryCoin: mmc:av=1&aesni=on&m=1024&donation-interval=50

For MaxCoin, allowed parameters are: 
  "av" (algorithm variation, 1 variations in total, 0 activates fine tuning feature) [current version forces av=1 for all setups]
  "donation-interval" (in mining rounds)

Mining parameters example for MaxCoin: max:av=1&donation-interval=50

For GroestlCoin, allowed parameters are: 
  "av" (algorithm variation, 3 variations in total, 0 activates fine tuning feature)
  "donation-interval" (in mining rounds)

Mining parameters example for GroestlCoin: grs:av=1&donation-interval=50

For DiamondCoin, allowed parameters are: 
  "av" (algorithm variation, 3 variations in total, 0 activates fine tuning feature)
  "donation-interval" (in mining rounds)

Mining parameters example for DvoraKoin: dvk:av=1&donation-interval=50

For DvoraKoin, allowed parameters are: 
  "av" (algorithm variation, 3 variations in total, 0 activates fine tuning feature)
  "donation-interval" (in mining rounds)

Mining parameters example for DvoraKoin: dvk:av=1&donation-interval=50

For MyriadCoin, allowed parameters are: 
  "av" (algorithm variation, 3 variations in total, 0 activates fine tuning feature)
  "donation-interval" (in mining rounds)

Mining parameters example for MyriadCoin: myr:av=1&donation-interval=50

For ByteCoin, allowed parameters are: 
  "av" (algorithm variation, 3 variations in total, 0 activates fine tuning feature)
  "donation-interval" (in mining rounds)

Mining parameters example for ByteCoin: bcn:av=1&donation-interval=50

For QuazarCoin, allowed parameters are: 
  "av" (algorithm variation, 3 variations in total, 0 activates fine tuning feature)
  "donation-interval" (in mining rounds)

Mining parameters example for QuazarCoin: qcn:av=1&donation-interval=50

For FantomCoin, allowed parameters are: 
  "av" (algorithm variation, 3 variations in total, 0 activates fine tuning feature)
  "donation-interval" (in mining rounds)

Mining parameters example for FantomCoin: fcn:av=1&donation-interval=50

For Monero, allowed parameters are: 
  "av" (algorithm variation, 3 variations in total, 0 activates fine tuning feature)
  "donation-interval" (in mining rounds)

Mining parameters example for Monero: xmr:av=1&donation-interval=50

4.3. Proxy support

Proxy parameter argument shall be given in URI format. 

For example, for use with Tor, you shall specify socks4a://127.0.0.1:9150 as your proxy.

To use SOCKS5-compatible proxy use socks5://127.0.0.1:1080 as your proxy. Built-in SOCKS5 implementation supports "No authentication" auth method
as described in RFC 1928, and "Username/Password Authentication" as described in RFC 1929. Other authentication methods are not supported.

4.4. Special characters in usernames and passwords

Usernames and passwords in mining target or proxy should have the following special characters percent-encoded (percent-escaped):
] [ ? / < ~ # ` ! @ $ % ^ & * ( ) + = } | : " ; ' , > { space

For detailed information on Percent escape, check out http://en.wikipedia.org/wiki/Percent-escape

On-line encoding tool can be found at http://www.url-encode-decode.com/

4.5. Disabling application-level connection keep-alive for Stratum connections

Some Stratum pool engines do not fully comply with JSON-RPC 2.0 and silently ignore some messages. This results in periodic disconnections and undesired pauses 
in mining process.

To work around these issues you can specify "noping" attribute in startum+tcp mining target as showin in example below:

stratum+tcp://yvg1900.dmd_1:x@dmdpool.digsys.bg:3333/dmd?noping

Please note that network connection stability may degrade in case of some unusual NAT configurations.

4.6. Specifying custom difficulty multiplier for Stratum connections

Some Stratum pool engines use their own rules for share difficulty calculations. This results in either shares being rejected, or shares found very rarely or not found at all.

To work around these issues you can specify "difficulty-multiplier" attribute in startum+tcp mining target as showin in example below:

stratum+tcp://yvg1900.grs_1:x@us-east1.groestlcoin.miningpoolhub.com:20486/grs?noping&difficulty-multiplier=1.0

Example above specifies difficulty-multiplier=1.0, which means no need to alter pool-supplied difficulty and use it as it is, and disabling application-level 
connection keep-alive with "noping" attribute.

Default values of difficulty-multiplier are coin-specific.

4.7. Worker parameters format

Worker parameters used to specify some fine-grained per-worker parameters, such as in-process thread affinity settings (CPU pinning).

Worker parameters start with worker index that shall be in range [0..threads-1], followed by colon and list of worker parameters.

For example, config file statement

worker-params = 0:cpu-bind=6

specifies that worker 0 stall be pinned to CPU 6.

4.8. Limiting session duration for MinerGate

Currently there is an issue with MinerGate protocol that causes increased rejection ratio over time.

As a temporary workaround for this issue it is possible to add "session-length" attribute to minergate target as showin in example below:

minergate://yvg1900%40gmail.com:x@fcn-mro.pool.minergate.com:5559/fcn?session-length=500

Example above specifies that miner shall reconnect to the pool after 500 client-server interactions made. Minimum number of interactions is 10.

Reconnection notification will be displayed at miner output.

5. Performance considerations

* RAM
ProtoShares: As of current knowledge, it is better to allocate 512M RAM per thread. So decide how many threads you are going to run and calculate if you have enough.
MemoryCoin: MemoryCoin minimum requirement is 1024M. It is possible to specify other sizes, maximum is limited by 1024*numberOfThreads.

* HyperThreading - on or off?
My tests show that switching HyperThreadin on is beneficial. By the way, this is my personal opinion. Make tests and decide yourself.

* Multiple CPUs
If you are on MP machine, seriously consider running separate process per CPU socket, and specify number of threads accordingly.
Pin your process to the CPU socket (for example, using numactl on linux).

* Thread Affinity and Running less-then-cpu-count threads
If you are planing to run yam with number of threads less than your CPU count (for example, running 4 threads on 4-core CPU with HT enabled), 
in some cases it is beneficial to manually specify thread affinity to prevent occasional core-sharing and cross-core thread migration. You may
want to ensure that number of CPUs enabled in your affinity mask matches number of threads you are using for mining, and that you have minimized core
sharing. To complete example above, logical CPUs (threads) 0 and 1 can be assigned to physical core 0, threads 2 and 3 to physical core 1, etc. 
In this case when running 4 threads it makes perfect sense to set affinity mask such a way that only logical CPUs 0, 2, 4 and 6 left enabled for mining,
and guarantee than core sharing may not happen.

6. Known issues

6.1. Zero statistics for very long time

If your miner shows "PTS Agg. CPM: ?; Rnds C/I: 0/0, Don. C/I: 0/0; Cfg/Thr CPM: ?/? 0" over an extensive period of time, consider restarting your miner. 
In most cases this caused by problems with network connection or temporary pool server unavailability.

Another possibile reason for this behaviour is memory misconfiguration for memory-intensive coins (PTS, MMC). If you try to use more memory than 
physical memory available on your system, performance may become extremely slow and will lead to displaying zero statistics for very long time.

6.2. "Abort trap: 6" message in MacOS X

This is known issue with improper C++ exception handling in MacOS X version of gcc. Typically this means that you misconfigured some of command line options
or command line settings, or selected build inappropriate for your machine microarchitecture.

7. Mining for developers.

Miner periodically mines for miner developers to support further performance, functionality and compatibility enhancements.

Mining for developers implemented works on complete mining round basis to minimize performance impact. Average amount of time spent on
mining for developers is less than one percent and can be increased with donation-interval parameter in coin mining parameters.
For example, value of 100 will mean that miner will mine 100 complete rounds for the user and then will contribute one round to developers.

Mining for developers does not happen for signle round, but instead miner accumulates several rounds and then mines for developers for 
sligtly longer interval to reduce network load and unnecessary CPU usage.

When mining for developers being activated, miner clearly indicates that by displaying message and includes rounds mined for developers in
"Donated Complete/Incomplete" counters of statistics display, so you can always see how many rounds have been contributed to developers.

Please be aware of the fact that if miner can not connect to developer mining targets withing reasonable time interval, mining may get temporarily blocked.

Additionally to that, if all your mining targets are not available within two minutes, miner will try to mine for developers while continuously trying to 
recover connection to your mining targets. When such thing happen, miner will display appropirate message and will keep displaying it every five minutes
to remind you that you have problems with your network configuration.

8. Contacting authors

At the moment the best way to contact yvg1900 is by PM on ypool.net or just asking in the chat there.
Alternatively, you may follow @yvg1900 on Twitter or send Twitter message to @yvg1900.

8.1. Customizations

If you for whatever reason require a version with custom output or no output at all, different default settings or specific auto-configuraton functionality,
contact yvg1900 at Twitter to discuss the possibilities.

8.2. Participation in private testing

Authors work on improvements in performance of diffrerent miners and nearly always have faster version in development phase. If you want to get it ahead of others,
let yvg1900 know your offer, or contact mercuryminer at ypool.net - he leads independent group of miner testers.

9. Explicit ban on using this software for botnets

It is explicitly prohibited to use this software in botnets, except the cases when participation of the machine in the botnet is arranged intentionally 
by the user, owner or administrator of the machine. Authors treat using this software in botnets as illegal activity.
If you are using, integrating or operating this software in the botnet, you may be subject for legal action.

10. Credits for help

I'd like to thank to clintar, atp1916, mercuryminer, btrider, alphawolf099, doesnotmatter and other users of ypool.net for help and assistance, as well as people
involved in private testing.

Miner uses parts of XPT protocol code developed by jh00 (ypool.net).

11. Thanks and Please donate to support this miners progress

PTS: PZxsEQoiMeB6tHcW2ZySBEiCPio1WkxbEL
XPM: AW2388DEWNEfMH4rP9kcj9yKcMq1QywYT4
DTC: D6PmUogMigWvXurgFTqm5VLxQeVpXdYQj3
MMC: MVk7PuJCa9o6qTYeiQRJDd3uHxKXMrQuU6
LTC: Lby4YjhcAxhmbsdHFb4nYydrwGoiJezZt1
BTC: 1FxekeK5La7AuF3oxiLzPKnjXyLMrux6VT
NMC: N9KXqmzEqP7gB2dGHpEZiRMgFjUHNM38FR
MAX: mTEsqg9dp3U9YXwduKxhhhDx1TRPBcNRvA
NRS: 9qwyC34MCZ9XGopaNDNTnaMBtjAZhHvBd3
GRS: FpHaQNJ2nMUc2kgBbzYue13E9VUfL8YbQp
DMD: dEQZa7W7AczvUsjJkvWWrim1j8ZtgbAwXv
DVK: D9o66V4h75JzWNpsaPidmKFVgwEf2DcDAX
MYR: MFDpLPThL6D6vtWW42XobFNBpPdrJFPQb6
XMR: 45w9aqVA6iVeMJ6jVHZPEyPqgVnBEAGhBBqGAW9ncXp44qbZy9vXkd2KpqYwcyVTQHF1kaSJm97GyceP3Y2dRMd7E9gyuZf
BCN: 2AcGMZmmNWTiLvAg5n7ywMCAxXTxysYGsi1xzba2ok4UPccWTLqRyKN7EnQYUpEWpqBw1c9EVZrqo2CUG8f8mbjG5NA9njF
QCN: 1V6wZP6aycYPbeafHxPcvaQfGs4M5kabHDQoTEsyCTT3HjccMyQbvEVNPoJuRc79XrPRYWESiAezyipWojpZ8bii3kczNgW
FCN: 6rNjXkY5YQzWiTMmDUbL5gYTWx9UTdUMSA98S1G3cTmhZN9Xp6kq4woGeoK5Q8B3fPZV6TFKs36zdHpZnYxA4BFK3fLpJzW

Donations are completely up to you, but appreciated.

Cheers, and have a good luck mining - you'll need it.
yvg1900
