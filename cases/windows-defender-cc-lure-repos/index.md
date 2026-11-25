# GitHub lure repos on aged batch-made accounts, and the information stealer one of their download chains delivers

Category: infrastructure-setup-patterns  
Published: 2026-11-20  
Write-up: https://github.com/scoope3/groundwork/tree/main/cases/windows-defender-cc-lure-repos

## Summary

GitHub accounts created on a handful of days in June, August and September 2026 each got one placeholder repository and were then left alone. From 2026-10-01 at the latest those accounts began carrying a lure: a README dressed as a free, "pre-activated" copy of commercial software that tells the reader to paste one command. 354 lure repositories are known: 113 from the first collection (105 still live on 2026-11-20) and 241 found on 2026-11-20 by reading the accounts numbered around the known owners. That second pass read only repositories pushed since 2026-10-01, so the count is a floor.

The lures use two groups of delivery hosts, and what this case says about the stealer applies to the first group only. For `devtools8[.]lol` (with `toolget2[.]lol`) and `quickrun31[.]cc` the chain was run end to end in a public Windows sandbox: a loader script, a password-protected RAR archive and an unpacker, then the program inside. For `ps-ps[.]cc`, `power-shell[.]cc`, `git-software[.]cc` and `windows-defender[.]cc` the scripts were never retrieved here and the hosts served nothing or no longer resolved on 2026-11-20. Other researchers report a different chain for `git-software[.]cc` (HiLleywyn/ward) and for an earlier host with the same script path (Zero-winter, 2026-09-04); what these lures deliver was not verified. `monolit[.]sbs` takes its archive from a file-sharing link and was not run on Windows.

The program is an information stealer with a download-and-run task feature. It exited within seconds in the sandbox. Its unpacked code was read statically: it checks for virtual machines, analysis tools and ten interface languages, and it is built to take browser data, wallets, password-manager and messenger data and developer secrets. It was never observed stealing anything. It decrypts its server address, `meta3[.]grovestack[.]one:443`, from a value built into the program, from a telegra[.]ph page and from a Polygon smart contract. The server was never contacted. A second build, delivered from `quickrun31[.]cc` on 2026-11-20, has its own key, page and contract and decrypts its server address to `log[.]travelvault[.]today:443`. Those values were reported by a separate static-analysis session, whose reading is also the basis for calling the two builds one family; the three decryptions were repeated here. That server was never contacted either.

The contract was created by a wallet that has created 188 contracts of nearly identical size since 2026-10-08. That all of them are resolvers of this kind is an inference from their size and pattern; only three are tied to a malware build (the two builds here and the sibling build). A sibling build from the same download host was analysed first by Ethan Kawley ([Ethan-Ka/toolget2-malware-analysis](https://github.com/Ethan-Ka/toolget2-malware-analysis), 2026-11-03); its contract comes from the same wallet, and its server is listed below as his finding. Much of the reported behaviour overlaps Elastic Security Labs' description of REVSTEALER, with differences, and Elastic's detection rule does not match this sample, so the family is an inference.

Three lures from 2026-11-17 also carry a macOS command for `appget29[.]tools`. In a public macOS sandbox the file it downloads profiled the machine and showed a fake "System Settings" password prompt. Its family and what it takes afterwards are not known.

Accounts of the same make, one of them in a creation batch shared with this case's owners, were also seen carrying a different lure kit on other hosts. The shape or batch of an account therefore does not show whose lure a repository holds; the host in the command does.

## Reading the indicators

- `lure_delivery_domain`, `next_stage_host`, `stealer_c2`: hosts. Five of the delivery hosts (`windows-defender[.]cc`, `power-shell[.]cc`, `powershell[.]lat`, `ps-ps[.]cc`, `git-software[.]cc`) are known only from README text; their scripts were never retrieved.
- `lure_repo`: the GitHub repositories carrying the lure, live when checked. They are evidence and a takedown list, not a claim about who owns the accounts.
- `dead_drop`, `resolver_contract`: a page on a public publishing service and a contract on a public blockchain. Block the specific page or watch for the specific call; do not block the services.
- `deployer_wallet`: kit scope. Whether the wallet belongs to one operator or to a service used by many is not known.
- `third_party_c2`: reported by another researcher and credited to him; not re-derived here.
- Files, in the order listed below: the loader script served at `devtools8[.]lol/j2sj9blzc` (PowerShell, 14,841 bytes, same hash in three sandbox runs); the loader script served at `monolit[.]sbs` (PowerShell, 4,819 bytes, retrieved 2026-11-18); the password-protected archive `67q65idtq.rar` served by `toolget2[.]lol` (3,286,078 bytes); and the stealer as delivered, `bh3xm14ke1.exe` (packed, self-signed, 3,460,200 bytes; hash reported by two analysis sessions). Then the second build as delivered from `quickrun31[.]cc`, `pt12owjk2s.exe` (packed, 2,622,928 bytes); its archive `l1d2va.rar` as served on 2026-11-20; and the macOS program served by `appget29[.]tools` (universal Mach-O, 811,040 bytes). The unpacker the loader downloads is reported to be a genuine UnRAR build and is deliberately not listed.

Nothing in this case is attributed to a person or group.

## Evidence

| Evidence type | Scope | False-positive rate | On |
| --- | --- | --- | --- |
| dead_drop | operator | 0% | `https://telegra.ph/Clear-ridge-11-10` |
| dead_drop | operator | 0% | `https://telegra.ph/Canvas-grove-11-19` |
| deployer_wallet | kit | 0% | `0x8bAddf058D11005360900a0542484eE446F2d494` |
| lure_delivery_domain | operator | 0% | `windows-defender.cc` |
| lure_delivery_domain | operator | 0% | `monolit.sbs` |
| lure_delivery_domain | operator | 0% | `devtools8.lol` |
| lure_delivery_domain | operator | 0% | `power-shell.cc` |
| lure_delivery_domain | operator | 0% | `powershell.lat` |
| lure_delivery_domain | operator | 0% | `ps-ps.cc` |
| lure_delivery_domain | operator | 0% | `git-software.cc` |
| lure_delivery_domain | operator | 0% | `quickrun31.cc` |
| lure_delivery_domain | operator | 0% | `appget29.tools` |
| lure_delivery_domain | operator | 0% | `pkgsetup.cc` |
| lure_repo | operator | 0% | `https://github.com/dreamtherapistcrypt/Chaos-Enscape-Collection-Free-Professional-3D-Rendering` |
| lure_repo | operator | 0% | `https://github.com/petacockatooblock/Chaos-Corona-Collection-Free-Professional-Architectural-Rendering` |
| lure_repo | operator | 0% | `https://github.com/Blizzardteawning/IK-Multimedia-AmpliTube-5-MAX-v2-Free-Guitar-Bass-Modeling` |
| lure_repo | operator | 0% | `https://github.com/Pondshoreproduce/Celemony-Melodyne-5-Studio-Free-Professional-Vocal-Tuning` |
| lure_repo | operator | 0% | `https://github.com/Scalarbatturn/Serato-DJ-Suite-Free-Professional-DJ-Software` |
| lure_repo | operator | 0% | `https://github.com/ChromePheasant/Neural-DSP-Plugins-Free-Professional-Guitar-Bass-Production` |
| lure_repo | operator | 0% | `https://github.com/Wayvontitle2/Autodesk-Revit-2027-Free-Professional-BIM-Software` |
| lure_repo | operator | 0% | `https://github.com/magentacrabsoul/Native-Instruments-Traktor-Pro-4-Free-Professional-DJ-Software` |
| lure_repo | operator | 0% | `https://github.com/RestrictionCarpenter/iZotope-RX-12-Advanced-Free-Professional-Audio-Restoration` |
| lure_repo | operator | 0% | `https://github.com/ratequeenask/Native-Instruments-Guitar-Rig-7-Pro-Free-Guitar-Amp-Effects` |
| lure_repo | operator | 0% | `https://github.com/Gloryfromcall/Steinberg-SpectraLayers-Pro-13-Free-AI-Audio-Editing` |
| lure_repo | operator | 0% | `https://github.com/gpujouninravine/rekordbox-Professional-7-Free-Professional-DJ-Software` |
| lure_repo | operator | 0% | `https://github.com/MinotaurByteBond10/Twinmotion-2026-Free-Professional-Architectural-Visualization` |
| lure_repo | operator | 0% | `https://github.com/SkyGeomancer/Chaos-V-Ray-Collection-Free-Professional-3D-Rendering` |
| lure_repo | operator | 0% | `https://github.com/Galaxyeitriumph/Graphisoft-Archicad-29-Collaborate-Free-Professional-BIM-Design` |
| lure_repo | operator | 0% | `https://github.com/spirebossrescue/D5-Render-Teams-3.1.1-Free-Professional-3D-Rendering` |
| lure_repo | operator | 0% | `https://github.com/SheetMythStretch/Vectorworks-Architect-2027-Free-Professional-BIM-Design` |
| lure_repo | operator | 0% | `https://github.com/existenceblazecanyon/SOLIDWORKS-Design-Ultimate-2026-Free-Professional-3D-CAD` |
| lure_repo | operator | 0% | `https://github.com/LavaDeerHook/Autodesk-Inventor-Professional-2027-Free-3D-CAD-Design` |
| lure_repo | operator | 0% | `https://github.com/AnalystSucceed/HWID-Testing-Utility-Free-Hardware-ID-Management` |
| lure_repo | operator | 0% | `https://github.com/CoalSmokeMake/voicemod` |
| lure_repo | operator | 0% | `https://github.com/PulverizeFrogFigure/voicemod` |
| lure_repo | operator | 0% | `https://github.com/FloodChemistQuilt/voicemod` |
| lure_repo | operator | 0% | `https://github.com/cliffmotormanvolt38/winutilits` |
| lure_repo | operator | 0% | `https://github.com/PeakEconomicFetter/Filmora16-Ai-Editor-Plus` |
| lure_repo | operator | 0% | `https://github.com/limetempodemodulator/Microsoft-Power-BI-Pro` |
| lure_repo | operator | 0% | `https://github.com/ColorsSwanFlare/After-Effects` |
| lure_repo | operator | 0% | `https://github.com/AreaCounselorFurnace/EaseUS-Todo-Backup` |
| lure_repo | operator | 0% | `https://github.com/ForestBladesmith/Adobe-Audition-PC` |
| lure_repo | operator | 0% | `https://github.com/Modernlavilla/GTA6-PC` |
| lure_repo | operator | 0% | `https://github.com/SolarMistSay/REAPER-7.84-Free-Professional-Audio-Production` |
| lure_repo | operator | 0% | `https://github.com/beatlarkknow/Foundry-Nuke-Studio-Free-Download-VFX-Software` |
| lure_repo | operator | 0% | `https://github.com/Entityoverregister/FL-Studio-Free-Download-Modified-Edition` |
| lure_repo | operator | 0% | `https://github.com/creekspiderwrench/Neat-Video-Professional-Video-Noise-Reduction` |
| lure_repo | operator | 0% | `https://github.com/marblecashierdeflate/Adobe-After-Effects-Modified-Edition` |
| lure_repo | operator | 0% | `https://github.com/SoundCourier/Steinberg-Cubase-Music-Production-Software` |
| lure_repo | operator | 0% | `https://github.com/Sandglodepot35/Boris-FX-Suite-VFX-Motion-Graphics` |
| lure_repo | operator | 0% | `https://github.com/RetroDukeGrasp/CapCut-Pro-Advanced-Video-Editing-Software` |
| lure_repo | operator | 0% | `https://github.com/Goliathvubarrier/VEGAS-Pro-Professional-Video-Editing-Software` |
| lure_repo | operator | 0% | `https://github.com/AttorneyPrime/DVDFab-Enlarger-AI-Free-AI-Video-Upscaling` |
| lure_repo | operator | 0% | `https://github.com/Celestialdenlure/DaVinci-Resolve-Studio-Video-Editing-Color-Grading` |
| lure_repo | operator | 0% | `https://github.com/beingtyrantdescribe/Wondershare-Filmora-Premium-Video-Editing-Software` |
| lure_repo | operator | 0% | `https://github.com/LovebirdQuest/Mocha-Pro-Free-Download-Motion-Tracking-VFX` |
| lure_repo | operator | 0% | `https://github.com/SpikeEmissary/Avid-Pro-Tools-Ultimate-Free-Professional-Audio-Production` |
| lure_repo | operator | 0% | `https://github.com/HighwayPixel/Avid-Media-Composer-Professional-Video-Editing` |
| lure_repo | operator | 0% | `https://github.com/SageSpanner84/Cavalry-Free-2D-Animation-Motion-Graphics-Software` |
| lure_repo | operator | 0% | `https://github.com/GlazeFighter9/Maschine-3-Bundle-Free-Beat-Making-Music-Production` |
| lure_repo | operator | 0% | `https://github.com/opencolonelswell/Bitwig-Studio-6-Free-Professional-Music-Production` |
| lure_repo | operator | 0% | `https://github.com/Capturebrifence/Adobe-Audition-26.5-Professional-Audio-Editing` |
| lure_repo | operator | 0% | `https://github.com/ChauffeurMoon91/FilmLight-Baselight-v7-Free-Professional-Color-Grading` |
| lure_repo | operator | 0% | `https://github.com/PanelLocksmithSquare/Blackmagic-Fusion-Studio-21-Free-Professional-VFX` |
| lure_repo | operator | 0% | `https://github.com/handcuffrajarepair/Adobe-Premiere-Pro-Free-Professional-Video-Editing` |
| lure_repo | operator | 0% | `https://github.com/macrosergeantsquare/Native-Instruments-Massive-X-1.7-Free-Professional-Synthesizer` |
| lure_repo | operator | 0% | `https://github.com/RealRegionKind/iZotope-Ozone-12-Advanced-Free-Professional-Audio-Mastering` |
| lure_repo | operator | 0% | `https://github.com/Psycheoftrim36/Spitfire-Audio-BBC-Symphony-Orchestra-Professional-Free` |
| lure_repo | operator | 0% | `https://github.com/Torrentdreinferno/EastWest-ComposerCloud-Free-Premium-Virtual-Instruments` |
| lure_repo | operator | 0% | `https://github.com/Slowgrerhythm/Xfer-Serum-2-Free-Professional-Wavetable-Synthesizer` |
| lure_repo | operator | 0% | `https://github.com/LusterJouninAtone25/Spectrasonics-Omnisphere-3-Free-Professional-Synthesizer` |
| lure_repo | operator | 0% | `https://github.com/BreezeFlamingoGorge/Sound-Forge-Plus-2026-Free-Professional-Audio-Editing` |
| lure_repo | operator | 0% | `https://github.com/ComponentSupplier/Waves-Ultimate-V17-Free-Professional-Audio-Plugins` |
| lure_repo | operator | 0% | `https://github.com/dreamcyclevoyage/Plugin-Alliance-PRO-Free-Professional-Audio-Plugins` |
| lure_repo | operator | 0% | `https://github.com/RouteShelter/Arturia-Pigments-7-Free-Professional-Synthesizer` |
| lure_repo | operator | 0% | `https://github.com/Shellfespiral/Native-Instruments-Kontakt-8-Full-Free-Professional-Sampler` |
| lure_repo | operator | 0% | `https://github.com/PointAirRecover56/Wise-Care` |
| lure_repo | operator | 0% | `https://github.com/Rhythmtrualter/Wise-Registrity` |
| lure_repo | operator | 0% | `https://github.com/silverindustrialgap/Auslogics` |
| lure_repo | operator | 0% | `https://github.com/RopemakerCoil/Burning-Studio` |
| lure_repo | operator | 0% | `https://github.com/sandsheriffbeat/Cinebench` |
| lure_repo | operator | 0% | `https://github.com/SegmentWarden/Data-Grip` |
| lure_repo | operator | 0% | `https://github.com/squareswimmeryell/Easy-Worship` |
| lure_repo | operator | 0% | `https://github.com/SplendorCooper/ExitLag` |
| lure_repo | operator | 0% | `https://github.com/StylistMultiplexer/HitFilm` |
| lure_repo | operator | 0% | `https://github.com/symboladvocateshaft/KeyShot-Pro` |
| lure_repo | operator | 0% | `https://github.com/VaultAssurance/PHP-Storm` |
| lure_repo | operator | 0% | `https://github.com/wellflashalter/RX-11-Audio-Editor` |
| lure_repo | operator | 0% | `https://github.com/vortexlakecanal/Rufus` |
| lure_repo | operator | 0% | `https://github.com/Wyrmfosafeguard/Sylenth-1` |
| lure_repo | operator | 0% | `https://github.com/yarnvoicedesignate/ultra-Iso` |
| lure_repo | operator | 0% | `https://github.com/MediatorRevive/CCleaner-Pro` |
| lure_repo | operator | 0% | `https://github.com/Attodreslicer/drphone-data-recovery` |
| lure_repo | operator | 0% | `https://github.com/56411952/aion-2-enhancement-suite` |
| lure_repo | operator | 0% | `https://github.com/foursixity001-hub/aion-2-enhancement-suite` |
| lure_repo | operator | 0% | `https://github.com/joaopedro903/delta-executor-desktop-toolkit` |
| lure_repo | operator | 0% | `https://github.com/GpiceQ/inventor-desktop-installer` |
| lure_repo | operator | 0% | `https://github.com/Hubkrereanimate/Secure-PDF-Workstation` |
| lure_repo | operator | 0% | `https://github.com/Omegaofidolize/ableton-live-12` |
| lure_repo | operator | 0% | `https://github.com/phantomsociallook/auslogics` |
| lure_repo | operator | 0% | `https://github.com/Pointyodemolish/bloxshade-for-roblox` |
| lure_repo | operator | 0% | `https://github.com/PlanetCraneInterface/autodesk-revit` |
| lure_repo | operator | 0% | `https://github.com/platooncaptainmarket/better-discord` |
| lure_repo | operator | 0% | `https://github.com/QuakeAdmiral/crash-plan` |
| lure_repo | operator | 0% | `https://github.com/ShackleCosmetologist/genesis-scanner` |
| lure_repo | operator | 0% | `https://github.com/shalecorporatelabel/grayket` |
| lure_repo | operator | 0% | `https://github.com/SmokeObliterate/imyfone` |
| lure_repo | operator | 0% | `https://github.com/SphereMagistrate39/metatrader` |
| lure_repo | operator | 0% | `https://github.com/TerminusPotter/quant-trading-bot` |
| lure_repo | operator | 0% | `https://github.com/VillageExecutive/ultra-edit` |
| lure_repo | operator | 0% | `https://github.com/VolcanoBaseCock/voicechanger` |
| lure_repo | operator | 0% | `https://github.com/WeaponsmithPray/winutilits` |
| lure_repo | operator | 0% | `https://github.com/WeaveSeekerJinx/wise-care` |
| lure_repo | operator | 0% | `https://github.com/Falsetervitalize/discord-server-raider` |
| lure_repo | operator | 0% | `https://github.com/gripdiplomatendure1/melodyne-5` |
| lure_repo | operator | 0% | `https://github.com/gryphonduckdefend/microsoft-office` |
| lure_repo | operator | 0% | `https://github.com/Grottoflachain/microsoft-365` |
| lure_repo | operator | 0% | `https://github.com/hopegiraffestride/movavi-video-editor-plus` |
| lure_repo | operator | 0% | `https://github.com/JumperCrater/pump-fun` |
| lure_repo | operator | 0% | `https://github.com/MechanicClaim/total-commander` |
| lure_repo | operator | 0% | `https://github.com/mortalswanstrait/wise-care` |
| lure_repo | operator | 0% | `https://github.com/DeimosPhobos666/office-suite-validator` |
| lure_repo | operator | 0% | `https://github.com/rimoharp/melodyne-5` |
| lure_repo | operator | 0% | `https://github.com/Unitphisignify/xswodvro` |
| lure_repo | operator | 0% | `https://github.com/driftcuttlefishjump/Serato-DJ-Pro` |
| lure_repo | operator | 0% | `https://github.com/armorsurgeonstill7/Clion` |
| lure_repo | operator | 0% | `https://github.com/PlotOtokageRespect/GrayKet` |
| lure_repo | operator | 0% | `https://github.com/ceilingforemanrank/CapCut-for-Windows` |
| lure_repo | operator | 0% | `https://github.com/BowyerSqueeze/Avid-Media-Composer` |
| lure_repo | operator | 0% | `https://github.com/fuserainday80/AOMEI-Backupper` |
| lure_repo | operator | 0% | `https://github.com/Sandstonetenoutfit/Cinebench` |
| lure_repo | operator | 0% | `https://github.com/Crestchadome/VoiceChanger` |
| lure_repo | operator | 0% | `https://github.com/Ninjaclaplunder36/AnyDesk` |
| lure_repo | operator | 0% | `https://github.com/rainfrogrectifier41/Avid-Media-Composer` |
| lure_repo | operator | 0% | `https://github.com/rainfrogrectifier41/Autodesk-3ds-MAX` |
| lure_repo | operator | 0% | `https://github.com/LimestoneCaptain/FabFilter-Total` |
| lure_repo | operator | 0% | `https://github.com/PinkTrackDesignate/Movavi-Video-Editor-Plus` |
| lure_repo | operator | 0% | `https://github.com/ApparitionElkCorrect/Wise-Care` |
| lure_repo | operator | 0% | `https://github.com/Colorstoserver/Movavi-Effects` |
| lure_repo | operator | 0% | `https://github.com/ShopkeeperConnector/Wise-Registrity` |
| lure_repo | operator | 0% | `https://github.com/frostaxetrough/Designcenter-NX` |
| lure_repo | operator | 0% | `https://github.com/WraithTellerSpout/Autodesk-3ds-MAX` |
| lure_repo | operator | 0% | `https://github.com/LevelSparkRecognize/Ashampoo-WinOptimizer` |
| lure_repo | operator | 0% | `https://github.com/Flashbylevel/FabFilter-Pro` |
| lure_repo | operator | 0% | `https://github.com/BlueProvostCrush/Quicken-Deluxe` |
| lure_repo | operator | 0% | `https://github.com/Volumetheboutique/Directory-Opus` |
| lure_repo | operator | 0% | `https://github.com/ViceAdvocate/ArchiCAD` |
| lure_repo | operator | 0% | `https://github.com/MajorShaperCultivate/Acronis` |
| lure_repo | operator | 0% | `https://github.com/MajorShaperCultivate/Ableton-Live-12` |
| lure_repo | operator | 0% | `https://github.com/BottomHeronEradicate/Movavi-Screen-Recorder` |
| lure_repo | operator | 0% | `https://github.com/FollowerPruner/Melodyne-5` |
| lure_repo | operator | 0% | `https://github.com/UnicornShade/PHP-Storm` |
| lure_repo | operator | 0% | `https://github.com/Demonsemarvel/Auslogics` |
| lure_repo | operator | 0% | `https://github.com/Icechiponder/SoundPad` |
| lure_repo | operator | 0% | `https://github.com/MortalGoldsmith40/Autodesk-Revit` |
| lure_repo | operator | 0% | `https://github.com/Topunderfeel/Ableton-Live-12` |
| lure_repo | operator | 0% | `https://github.com/Topunderfeel/Acronis` |
| lure_repo | operator | 0% | `https://github.com/StoneParakeet/Movavi-Video-Suite-Plus` |
| lure_repo | operator | 0% | `https://github.com/EastShipperRestore/SonyVegas` |
| lure_repo | operator | 0% | `https://github.com/beastofficerfollow/Movavi-Photo-Editor` |
| lure_repo | operator | 0% | `https://github.com/LizardScissors/Adobe-Acrobat-Pro` |
| lure_repo | operator | 0% | `https://github.com/metropolisorioletap/Adobe-InDesign` |
| lure_repo | operator | 0% | `https://github.com/metropolisorioletap/Actual-Multiplie-Monitors` |
| lure_repo | operator | 0% | `https://github.com/Lineureliminate/HitFilm` |
| lure_repo | operator | 0% | `https://github.com/PillarStreamPipe/Burning-Studio` |
| lure_repo | operator | 0% | `https://github.com/Matterwithinbastion/Data-Grip` |
| lure_repo | operator | 0% | `https://github.com/GaleVeterinarian/Power-Director` |
| lure_repo | operator | 0% | `https://github.com/DimCommercialFactory/Start11` |
| lure_repo | operator | 0% | `https://github.com/GlueRealmProduce/Cellebrite-UFED` |
| lure_repo | operator | 0% | `https://github.com/EmirOvercome/Adobe-After-Effects` |
| lure_repo | operator | 0% | `https://github.com/MagicArbiter/Easy-Worship` |
| lure_repo | operator | 0% | `https://github.com/PersonalityWalker/Movavi-Converter` |
| lure_repo | operator | 0% | `https://github.com/AdmiralDiscriminate/Photo-Commander` |
| lure_repo | operator | 0% | `https://github.com/holeconductorcrush/Kontakt-8` |
| lure_repo | operator | 0% | `https://github.com/hubdragonminaret/VoiceMod` |
| lure_repo | operator | 0% | `https://github.com/Windaurotation/Canva-Pro` |
| lure_repo | operator | 0% | `https://github.com/Windaurotation/Better-Discord` |
| lure_repo | operator | 0% | `https://github.com/Capitalaosteeple24/sbzjbgdy` |
| lure_repo | operator | 0% | `https://github.com/kindguruboost/Data-Grip` |
| lure_repo | operator | 0% | `https://github.com/HiddenSparrowMinaret/Wise-Registrity` |
| lure_repo | operator | 0% | `https://github.com/FoalShrink50/Movavi-Effects` |
| lure_repo | operator | 0% | `https://github.com/Weavebennurture/Burning-Studio` |
| lure_repo | operator | 0% | `https://github.com/Weavebennurture/Avid-Media-Composer` |
| lure_repo | operator | 0% | `https://github.com/Lineinmonitor/Ozone-12-Advanced` |
| lure_repo | operator | 0% | `https://github.com/PortionHelmsman/Movavi-Converter` |
| lure_repo | operator | 0% | `https://github.com/ashcustodiandolmen/Cinebench` |
| lure_repo | operator | 0% | `https://github.com/TrackViceCraft/Movavi-Video-Editor-Plus` |
| lure_repo | operator | 0% | `https://github.com/BayAssociate/Directory-Opus` |
| lure_repo | operator | 0% | `https://github.com/sharpbytekey/Movavi-Video-Suite-Plus` |
| lure_repo | operator | 0% | `https://github.com/SavageSamuraiTuck/CorelDraw` |
| lure_repo | operator | 0% | `https://github.com/PeltPythonCall/GrayKet` |
| lure_repo | operator | 0% | `https://github.com/Griffinlyatreasure85/Cellebrite-UFED` |
| lure_repo | operator | 0% | `https://github.com/Thornonanchorage/Ashampoo-WinOptimizer` |
| lure_repo | operator | 0% | `https://github.com/MarshalTrench/SonyVegas` |
| lure_repo | operator | 0% | `https://github.com/snatchbytesalvage/CCleaner-Pro` |
| lure_repo | operator | 0% | `https://github.com/SaboteurClip/Rufus` |
| lure_repo | operator | 0% | `https://github.com/JoinBardColonnade/RX-11-Audio-Editor` |
| lure_repo | operator | 0% | `https://github.com/PlanetPhaseRaid/VoiceMod` |
| lure_repo | operator | 0% | `https://github.com/Openbygather/Movavi-Photo-Editor` |
| lure_repo | operator | 0% | `https://github.com/ScrewDiverHike/Power-Director` |
| lure_repo | operator | 0% | `https://github.com/Ratiokrunote/Movavi-Converter` |
| lure_repo | operator | 0% | `https://github.com/SlateElementalist/SystemCare-Pro` |
| lure_repo | operator | 0% | `https://github.com/Minotaurtruflex/Microsoft-Project` |
| lure_repo | operator | 0% | `https://github.com/MelodySwimmer/Ultra-Edit` |
| lure_repo | operator | 0% | `https://github.com/Openyodepict/Movavi-Video-Editor-Plus` |
| lure_repo | operator | 0% | `https://github.com/EssenceConductor/Movavi-Video-Suite-Plus` |
| lure_repo | operator | 0% | `https://github.com/crimsonoriolehovel/Movavi-Effects` |
| lure_repo | operator | 0% | `https://github.com/HornbillJournal/Photo-Commander` |
| lure_repo | operator | 0% | `https://github.com/TarantulaKnow/Movavi-Screen-Recorder` |
| lure_repo | operator | 0% | `https://github.com/StreetGateChisel/Uttorent` |
| lure_repo | operator | 0% | `https://github.com/PathTailorRadial/StartAll-Back` |
| lure_repo | operator | 0% | `https://github.com/portalthunderphase/Movavi-Photo-Editor` |
| lure_repo | operator | 0% | `https://github.com/ExistenceProduction/Auslogics` |
| lure_repo | operator | 0% | `https://github.com/PaintShrimpDawn/Canva-Pro` |
| lure_repo | operator | 0% | `https://github.com/MailJudgeView/SoundPad` |
| lure_repo | operator | 0% | `https://github.com/Ponddergenerate/Movavi-Video-Suite-Plus` |
| lure_repo | operator | 0% | `https://github.com/ChainWizardAura/Cinebench` |
| lure_repo | operator | 0% | `https://github.com/SmartThunderDisplay/Movavi-Screen-Recorder` |
| lure_repo | operator | 0% | `https://github.com/FlowBeetle94/Autodesk-Revit` |
| lure_repo | operator | 0% | `https://github.com/Towerthroughlabel/FabFilter-Total` |
| lure_repo | operator | 0% | `https://github.com/BlacksmithColumn/AOMEI-Backupper` |
| lure_repo | operator | 0% | `https://github.com/FaceDuckStove/CapCut-for-Windows` |
| lure_repo | operator | 0% | `https://github.com/ringorcastay/Ashampoo-WinOptimizer` |
| lure_repo | operator | 0% | `https://github.com/SerpentCleric/Uttorent` |
| lure_repo | operator | 0% | `https://github.com/volumesamuraichill/SystemCare-Pro` |
| lure_repo | operator | 0% | `https://github.com/NightBiomancer/Cellebrite-UFED` |
| lure_repo | operator | 0% | `https://github.com/Grandmasterofend/Melodyne-5` |
| lure_repo | operator | 0% | `https://github.com/mudcoxswainpit/Movavi-Converter` |
| lure_repo | operator | 0% | `https://github.com/GiraffeCondense/Burning-Studio` |
| lure_repo | operator | 0% | `https://github.com/ShoreRealm72/RX-11-Audio-Editor` |
| lure_repo | operator | 0% | `https://github.com/WharfStarHike/Wise-Registrity` |
| lure_repo | operator | 0% | `https://github.com/BladesmithFirewall/KeyShot-Pro` |
| lure_repo | operator | 0% | `https://github.com/GraphLoopGame/FabFilter-Pro` |
| lure_repo | operator | 0% | `https://github.com/DragonHokageDecoder/Total-Commander` |
| lure_repo | operator | 0% | `https://github.com/Tracksiawning/VoiceMod` |
| lure_repo | operator | 0% | `https://github.com/chaindictatorpalace/AnyDesk` |
| lure_repo | operator | 0% | `https://github.com/Obsidiangrohoist/HitFilm` |
| lure_repo | operator | 0% | `https://github.com/Ditcharbarrier/ExitLag` |
| lure_repo | operator | 0% | `https://github.com/FigureNetworkConsole/Movavi-Video-Editor-Plus` |
| lure_repo | operator | 0% | `https://github.com/FenceSpinnerGuide/Rufus` |
| lure_repo | operator | 0% | `https://github.com/bittsuchikagelaud/Avid-Media-Composer` |
| lure_repo | operator | 0% | `https://github.com/Earthyodeliver16/Power-Director` |
| lure_repo | operator | 0% | `https://github.com/StreetMarine/Autodesk-3ds-MAX` |
| lure_repo | operator | 0% | `https://github.com/FinalJourneyman/Movavi-Effects` |
| lure_repo | operator | 0% | `https://github.com/megasheriffswell/Photo-Commander` |
| lure_repo | operator | 0% | `https://github.com/ClawFollowerMall/Chief-Architect-Premier` |
| lure_repo | operator | 0% | `https://github.com/torrentclassbay/SonyVegas` |
| lure_repo | operator | 0% | `https://github.com/oillovebirdbuild/Total-Commander` |
| lure_repo | operator | 0% | `https://github.com/ProviderRelease64/WinUtilits` |
| lure_repo | operator | 0% | `https://github.com/pentagongeneralgaze/VoiceChanger` |
| lure_repo | operator | 0% | `https://github.com/PheasantMetro/Uttorent` |
| lure_repo | operator | 0% | `https://github.com/opticantbarrow/Ultra-Edit` |
| lure_repo | operator | 0% | `https://github.com/silverofficialdusk/Easeus-Todo-Backup-For-Windows` |
| lure_repo | operator | 0% | `https://github.com/sparkfiremancollar21/Microsoft-Project-For-Windows` |
| lure_repo | operator | 0% | `https://github.com/BetaChampionTitle/Coreldraw-For-Windows` |
| lure_repo | operator | 0% | `https://github.com/StitchSerfJump/Microsoft-Visio-For-Windows` |
| lure_repo | operator | 0% | `https://github.com/DeckhandIgnite/Davinci-Resolve-Studio-For-Windows` |
| lure_repo | operator | 0% | `https://github.com/ElementalistTurbine/Ccleaner-Professional-For-Windows` |
| lure_repo | operator | 0% | `https://github.com/MudTsuchikage/Fl-Studio-For-Windows` |
| lure_repo | operator | 0% | `https://github.com/OrangeSaviorImagine/Abbyy-Finereader-Pdf-For-Windows` |
| lure_repo | operator | 0% | `https://github.com/Velocityatrhythm/Autodesk-3ds-Max-For-Windows` |
| lure_repo | operator | 0% | `https://github.com/MortarBeetleStyle/Autocad-For-Windows` |
| lure_repo | operator | 0% | `https://github.com/CatchArtisanDone86/Movavi-Video-Editor-For-Windows` |
| lure_repo | operator | 0% | `https://github.com/Sandsisupervise20/Adobe-Premiere-Pro-For-Windows-And-Macos` |
| lure_repo | operator | 0% | `https://github.com/gleameconomicjetty/Adobe-Indesign-For-Windows-And-Macos` |
| lure_repo | operator | 0% | `https://github.com/ManeSwordGraph/Adobe-Lightroom-Classic-For-Windows-And-Macos` |
| lure_repo | operator | 0% | `https://github.com/Cachewithinmake/GTA6-Preload-PC` |
| lure_repo | operator | 0% | `https://github.com/SageAdapter8/Rob-Run-Mod-Menu` |
| lure_repo | operator | 0% | `https://github.com/Weavedrobless13/Actual-Multiplie-Monitors` |
| lure_repo | operator | 0% | `https://github.com/Weavedrobless13/Acronis` |
| lure_repo | operator | 0% | `https://github.com/Wireearadial/Adobe-After-Effects` |
| lure_repo | operator | 0% | `https://github.com/Wireearadial/Actual-Multiplie-Monitors` |
| lure_repo | operator | 0% | `https://github.com/WharfBeetleGallery37/Acronis` |
| lure_repo | operator | 0% | `https://github.com/WharfBeetleGallery37/Ableton-Live-12` |
| lure_repo | operator | 0% | `https://github.com/ShaleNurseBurst/Wise-Registrity` |
| lure_repo | operator | 0% | `https://github.com/ManufacturingTurbine/Serato-DJ-Pro` |
| lure_repo | operator | 0% | `https://github.com/BondFletcher/Ashampoo-WinOptimizer` |
| lure_repo | operator | 0% | `https://github.com/angleartisanstitch/SystemCare-Pro` |
| lure_repo | operator | 0% | `https://github.com/JoinDamselReduce/Movavi-Video-Suite-Plus` |
| lure_repo | operator | 0% | `https://github.com/beastcrewmanraise56/AutoCad` |
| lure_repo | operator | 0% | `https://github.com/CaptainFurnish/AOMEI-Backupper` |
| lure_repo | operator | 0% | `https://github.com/celestialsteamsupply/Movavi-Video-Suite-Plus` |
| lure_repo | operator | 0% | `https://github.com/PathSwallowLock/Wise-Care` |
| lure_repo | operator | 0% | `https://github.com/BrokerSpiral/CapCut-for-Windows` |
| lure_repo | operator | 0% | `https://github.com/convergeattorneyquay/Claude-Jailbreak-Prompt` |
| lure_repo | operator | 0% | `https://github.com/Holeyospindle/Movavi-Effects` |
| lure_repo | operator | 0% | `https://github.com/Polygonglicavity/FL-Studio` |
| lure_repo | operator | 0% | `https://github.com/Sandstonelunamode/Autodesk-Revit` |
| lure_repo | operator | 0% | `https://github.com/MatrixSeaCode25/SketchUp-Pro` |
| lure_repo | operator | 0% | `https://github.com/HarborAxolotl/Kontakt-8` |
| lure_repo | operator | 0% | `https://github.com/StoragePupaAgitate/CorelDraw` |
| lure_repo | operator | 0% | `https://github.com/Magicvanmemorialize/Quicken-Deluxe` |
| lure_repo | operator | 0% | `https://github.com/OfficialHook/VoiceChanger` |
| lure_repo | operator | 0% | `https://github.com/NoviceBandage/Ashampoo-Uninstaller` |
| lure_repo | operator | 0% | `https://github.com/TrapSilversmith/KeyShot-Pro` |
| lure_repo | operator | 0% | `https://github.com/beamcrystalplunder/Actual-Multiplie-Monitors` |
| lure_repo | operator | 0% | `https://github.com/CassowaryMansion/Autodesk-CFD` |
| lure_repo | operator | 0% | `https://github.com/BadgeHealerConverter/Adobe-After-Effects` |
| lure_repo | operator | 0% | `https://github.com/Fabledandtrowel/Claude-Jailbreak-Prompt` |
| lure_repo | operator | 0% | `https://github.com/ExaMajorYell/FabFilter-Pro` |
| lure_repo | operator | 0% | `https://github.com/SphereIguana8/AutoCad` |
| lure_repo | operator | 0% | `https://github.com/legendaryturkeyspark/Ozone-12-Advanced` |
| lure_repo | operator | 0% | `https://github.com/azurepikemandivide/GrayKet` |
| lure_repo | operator | 0% | `https://github.com/GraphSoldierPergola/Instagram-Liker-Bot` |
| lure_repo | operator | 0% | `https://github.com/DensityCooper/Designcenter-NX` |
| lure_repo | operator | 0% | `https://github.com/FlowScorpion/HitFilm` |
| lure_repo | operator | 0% | `https://github.com/Feelingubattle/FL-Studio` |
| lure_repo | operator | 0% | `https://github.com/Characternearequip/CCleaner-Pro` |
| lure_repo | operator | 0% | `https://github.com/mintconductorzen/SonyVegas` |
| lure_repo | operator | 0% | `https://github.com/colonylightsever/Cinebench` |
| lure_repo | operator | 0% | `https://github.com/bodyconquerorclimb/Adobe-Substance-3d` |
| lure_repo | operator | 0% | `https://github.com/heightsongsouk/Microsoft-365` |
| lure_repo | operator | 0% | `https://github.com/Cacheacrossregain/Auslogics` |
| lure_repo | operator | 0% | `https://github.com/phantombudgiesheave/Wise-Registrity` |
| lure_repo | operator | 0% | `https://github.com/Arenadensocket/Data-Grip` |
| lure_repo | operator | 0% | `https://github.com/ChampionHaulerFlue/Burning-Studio` |
| lure_repo | operator | 0% | `https://github.com/Ensignchetrap/Easy-Worship` |
| lure_repo | operator | 0% | `https://github.com/NightingaleHinge/CCleaner-Pro` |
| lure_repo | operator | 0% | `https://github.com/FabledEmpressFree19/FabFilter-Total` |
| lure_repo | operator | 0% | `https://github.com/Coaliocontact/Chief-Architect-Premier` |
| lure_repo | operator | 0% | `https://github.com/hornsurgeontweezers/Movavi-Converter` |
| lure_repo | operator | 0% | `https://github.com/anglemayorwinch30/ArchiCAD` |
| lure_repo | operator | 0% | `https://github.com/Topazchosouk/Autodesk-Inventor` |
| lure_repo | operator | 0% | `https://github.com/BarbTernCrack/Acronis` |
| lure_repo | operator | 0% | `https://github.com/wyrmlawyerberth/Catia-Cad` |
| lure_repo | operator | 0% | `https://github.com/Highwayphomoon/Microsoft-Visio` |
| lure_repo | operator | 0% | `https://github.com/Dockuafill99/Directory-Opus` |
| lure_repo | operator | 0% | `https://github.com/BeamHornetStation/Adobe-Photoshop` |
| lure_repo | operator | 0% | `https://github.com/OceanViceIgnite97/Cinebench` |
| lure_repo | operator | 0% | `https://github.com/DustInterest/Ashampoo-WinOptimizer` |
| lure_repo | operator | 0% | `https://github.com/Captureglewharf/Autodesk-Inventor` |
| lure_repo | operator | 0% | `https://github.com/stratumvaporrecall/Melodyne-5` |
| lure_repo | operator | 0% | `https://github.com/OperativeNegotiator/WinUtilits` |
| lure_repo | operator | 0% | `https://github.com/Ambereuform65/Adobe-Acrobat-Pro` |
| lure_repo | operator | 0% | `https://github.com/MagentaMonetary/PHP-Storm` |
| lure_repo | operator | 0% | `https://github.com/Stuccoflarear/Burning-Studio` |
| lure_repo | operator | 0% | `https://github.com/GraspEmissaryKiln/Ads-Blocker` |
| lure_repo | operator | 0% | `https://github.com/Mortalveamend/StartAll-Back` |
| lure_repo | operator | 0% | `https://github.com/cascadefireflychill/Instagram-Liker-Bot` |
| lure_repo | operator | 0% | `https://github.com/DecaStudentIncrease/Data-Grip` |
| lure_repo | operator | 0% | `https://github.com/GripEmuSupply/FabFilter-Total` |
| lure_repo | operator | 0% | `https://github.com/MarineBridge/RX-11-Audio-Editor` |
| lure_repo | operator | 0% | `https://github.com/Centisaintpuzzle/Autodesk-Revit` |
| lure_repo | operator | 0% | `https://github.com/TheaterOcean/ExitLag` |
| lure_repo | operator | 0% | `https://github.com/beattestingdisplay/Directory-Opus` |
| lure_repo | operator | 0% | `https://github.com/CenterBorder/Imei-Repair` |
| lure_repo | operator | 0% | `https://github.com/Hidefitzoscillate/Microsoft-Project` |
| lure_repo | operator | 0% | `https://github.com/HectoGoldsmith/Melodyne-5` |
| lure_repo | operator | 0% | `https://github.com/Copperrutrim/AnyUnlock` |
| lure_repo | operator | 0% | `https://github.com/beachactivistmanor/Adobe-Audition` |
| lure_repo | operator | 0% | `https://github.com/tunnelowlcutters/Display-Fusion` |
| lure_repo | operator | 0% | `https://github.com/TrueSkyTassel/Auslogics` |
| lure_repo | operator | 0% | `https://github.com/flattoucanphase/GrayKet` |
| lure_repo | operator | 0% | `https://github.com/CommercialRuminate/Autodesk-CFD` |
| lure_repo | operator | 0% | `https://github.com/PurpleStationCharge/AnyDesk` |
| lure_repo | operator | 0% | `https://github.com/exajackdawmall/ExitLag` |
| lure_repo | operator | 0% | `https://github.com/LimestoneTellerHover/Serato-DJ-Pro` |
| lure_repo | operator | 0% | `https://github.com/BasiliskBrakemanMoon/ArchiCAD` |
| lure_repo | operator | 0% | `https://github.com/barrierpilotcatalog/Ads-Blocker` |
| lure_repo | operator | 0% | `https://github.com/NodeRajaCrater/Cellebrite-UFED` |
| lure_repo | operator | 0% | `https://github.com/trueparakeetadmire63/AOMEI-Backupper` |
| lure_repo | operator | 0% | `https://github.com/NinjaLynxFlow/SystemCare-Pro` |
| lure_repo | operator | 0% | `https://github.com/VectorMotorman/Clion` |
| lure_repo | operator | 0% | `https://github.com/monsterroguecontinue/Start11` |
| lure_repo | operator | 0% | `https://github.com/Monstereuraise/Audition-Pc` |
| lure_repo | operator | 0% | `https://github.com/WraithSheikh/stellar-recovery-hard-disk` |
| lure_repo | operator | 0% | `https://github.com/FuseVanquisher/dex-screener-crypto-analytics` |
| lure_repo | operator | 0% | `https://github.com/GhostMeadowlark/EaseUS-Todo-Backup` |
| lure_repo | operator | 0% | `https://github.com/WeightAlbatross/Uipath-Studio` |
| lure_repo | operator | 0% | `https://github.com/LoopPresident/aion-2-bot-auto-farm-optimizer` |
| lure_repo | operator | 0% | `https://github.com/Portionshuupgrade/wardogs-cheat-game-trainer` |
| lure_repo | operator | 0% | `https://github.com/leveetempoemancipate/Power-Bio-PC-Full` |
| lure_repo | operator | 0% | `https://github.com/GlowPolitician/rust-scripts-automation-tools` |
| lure_repo | operator | 0% | `https://github.com/Tabooonchain/slay-the-spire-2-mods` |
| lure_repo | operator | 0% | `https://github.com/LookoutVisionRivet/path-of-exile-2-bot` |
| lure_repo | operator | 0% | `https://github.com/momentumtiername/-xsplit-broadcaster` |
| lure_repo | operator | 0% | `https://github.com/PharaohManage/construct3` |
| lure_repo | operator | 0% | `https://github.com/PinTechnicianBang/ets2-mods-trainer` |
| lure_repo | operator | 0% | `https://github.com/PhysicianDominate/marvel-rivals-skin-changer-tools` |
| lure_repo | operator | 0% | `https://github.com/gridloaderrepair/Vmix-Pro` |
| lure_repo | operator | 0% | `https://github.com/TremorRider54/FMOD-Studio` |
| lure_repo | operator | 0% | `https://github.com/SpikeAxolotl/FL-STUDIO-PC` |
| lure_repo | operator | 0% | `https://github.com/BeetleRemain/gta-6-pc-download` |
| lure_repo | operator | 0% | `https://github.com/BehemothDyer/stable-diffusion-atelier` |
| lure_repo | operator | 0% | `https://github.com/Brinkoversteeple/docker-compose-stash` |
| lure_repo | operator | 0% | `https://github.com/EmissaryHike/jellyfin-media-notebook` |
| lure_repo | operator | 0% | `https://github.com/Glosszumlattice/quickbooks-ledger-alts` |
| lure_repo | operator | 0% | `https://github.com/Hubarsalvage/nintendo-switch-emulation-desk` |
| lure_repo | operator | 0% | `https://github.com/OutpostPython/tableau-viz-gallery` |
| lure_repo | operator | 0% | `https://github.com/Tensorflearcade/ps5-backup-saver` |
| lure_repo | operator | 0% | `https://github.com/VendorShelter/telegram-bot-foundry` |
| lure_repo | operator | 0% | `https://github.com/VillagePrefect/stable-diffusion-atelier` |
| lure_repo | operator | 0% | `https://github.com/WindServiceIdentify/ableton-production-bench` |
| lure_repo | operator | 0% | `https://github.com/grottosanninvoyage/k8s-homelab-sailor` |
| lure_repo | operator | 0% | `https://github.com/nora-herrera49/ADlabs-toolz` |
| lure_repo | operator | 0% | `https://github.com/polygondomainport/obs-streamer-stack` |
| lure_repo | operator | 0% | `https://github.com/silverbeatcompute/jellyfin-media-notebook` |
| lure_repo | operator | 0% | `https://github.com/superstormfringe/autohotkey-trove` |
| lure_repo | operator | 0% | `https://github.com/KrakenCraneCraft/Wirecast-Version-Pro` |
| lure_repo | operator | 0% | `https://github.com/ProsecutorSpade/Premier-Version-Pro` |
| lure_repo | operator | 0% | `https://github.com/Woodglodisclose/DXO-PHOTOLAB-10-ELITE` |
| lure_repo | operator | 0% | `https://github.com/TrenchZebraMaster/Capture-One-Pro` |
| lure_repo | operator | 0% | `https://github.com/Streetthetent33/Avid-Pro-Tools-Ultimate` |
| lure_repo | operator | 0% | `https://github.com/trapworkerravine/Davinci-resolve-version-pro` |
| lure_repo | operator | 0% | `https://github.com/WildCooperYank/vMix-Pro` |
| lure_repo | operator | 0% | `https://github.com/LogoGunsmithSteeple/siemens-nx-full-version` |
| lure_repo | operator | 0% | `https://github.com/onyxformvise/Autodesk-Revit-Full-Version` |
| lure_repo | operator | 0% | `https://github.com/SeniorExemplify/Adobe-Illustrator-Full-Version` |
| lure_repo | operator | 0% | `https://github.com/CorporateAxle/Steinberg-Nuendo-Full-version` |
| lure_repo | operator | 0% | `https://github.com/protonemuseparator/catia-3dexperience-full-version` |
| lure_repo | operator | 0% | `https://github.com/SpeedGiraffeWatt96/CorelDRAW-Graphics-Suite` |
| lure_repo | operator | 0% | `https://github.com/Followerpuvault/Autodesk-AutoCAD-Full-Version` |
| lure_repo | operator | 0% | `https://github.com/Matrixacrosscompact/SideFX-Houdini-FX-Full-Version` |
| lure_repo | operator | 0% | `https://github.com/ViceDeveloper/ivcam-full-version` |
| lure_repo | operator | 0% | `https://github.com/AmbassadorHonor/Autodesk-Maya-Full-Version` |
| lure_repo | operator | 0% | `https://github.com/Aquaunbungalow/Autodesk-3ds-max-full-version` |
| lure_repo | operator | 0% | `https://github.com/Plumemccharge/Maxon-ZBrush-Full-Version` |
| lure_repo | operator | 0% | `https://github.com/Watertrestring/camo-studio-pro-full-version` |
| lure_repo | operator | 0% | `https://github.com/wildswiftintroduce/rob-run-mod-menu-zoel` |
| lure_repo | operator | 0% | `https://github.com/GlossConstableShears/Unity-Pro-Full-Version` |
| lure_repo | operator | 0% | `https://github.com/FloorHelmsmanAxle95/-Grand-Theft-Auto-VI-preload-pc` |
| lure_repo | operator | 0% | `https://github.com/Modernuovacuum/gamemaker-professional-full-version` |
| lure_repo | operator | 0% | `https://github.com/blazeclientvise/rob-run-tools` |
| lure_repo | operator | 0% | `https://github.com/PeakNegotiatorKiln/Grand-Version-6` |
| lure_repo_template | kit | 0% | `github-repo-set:windows-defender-cc` |
| next_stage_host | operator | 0% | `toolget2.lol` |
| resolver_contract | operator | 0% | `0x1ee6A331881102B84d2DebdD5eefd2E591a65f14` |
| resolver_contract | operator | 0% | `0x45a7B8fAec623508bd68be535Cc7618f283ddB48` |
| star_inflation_pattern | context | 0% | `github-account-batch:2026-08-10` |
| stealer_c2 | operator | 0% | `meta3.grovestack.one` |
| stealer_c2 | operator | 0% | `log.travelvault.today` |
| third_party_c2 | kit | 0% | `scheduler.echoform32.club` |

## Indicators

| Type | Indicator | Evidence |
| --- | --- | --- |
| domain | `windows-defender.cc` | lure_delivery_domain |
| domain | `monolit.sbs` | lure_delivery_domain |
| domain | `devtools8.lol` | lure_delivery_domain |
| domain | `toolget2.lol` | next_stage_host |
| domain | `power-shell.cc` | lure_delivery_domain |
| domain | `powershell.lat` | lure_delivery_domain |
| domain | `meta3.grovestack.one` | stealer_c2 |
| url | `https://telegra.ph/Clear-ridge-11-10` | dead_drop |
| contract_address | `0x1ee6A331881102B84d2DebdD5eefd2E591a65f14` | resolver_contract |
| crypto_address | `0x8bAddf058D11005360900a0542484eE446F2d494` | deployer_wallet |
| domain | `scheduler.echoform32.club` | third_party_c2 |
| url | `https://github.com/dreamtherapistcrypt/Chaos-Enscape-Collection-Free-Professional-3D-Rendering` | lure_repo |
| url | `https://github.com/petacockatooblock/Chaos-Corona-Collection-Free-Professional-Architectural-Rendering` | lure_repo |
| url | `https://github.com/Blizzardteawning/IK-Multimedia-AmpliTube-5-MAX-v2-Free-Guitar-Bass-Modeling` | lure_repo |
| url | `https://github.com/Pondshoreproduce/Celemony-Melodyne-5-Studio-Free-Professional-Vocal-Tuning` | lure_repo |
| url | `https://github.com/Scalarbatturn/Serato-DJ-Suite-Free-Professional-DJ-Software` | lure_repo |
| url | `https://github.com/ChromePheasant/Neural-DSP-Plugins-Free-Professional-Guitar-Bass-Production` | lure_repo |
| url | `https://github.com/Wayvontitle2/Autodesk-Revit-2027-Free-Professional-BIM-Software` | lure_repo |
| url | `https://github.com/magentacrabsoul/Native-Instruments-Traktor-Pro-4-Free-Professional-DJ-Software` | lure_repo |
| url | `https://github.com/RestrictionCarpenter/iZotope-RX-12-Advanced-Free-Professional-Audio-Restoration` | lure_repo |
| url | `https://github.com/ratequeenask/Native-Instruments-Guitar-Rig-7-Pro-Free-Guitar-Amp-Effects` | lure_repo |
| url | `https://github.com/Gloryfromcall/Steinberg-SpectraLayers-Pro-13-Free-AI-Audio-Editing` | lure_repo |
| url | `https://github.com/gpujouninravine/rekordbox-Professional-7-Free-Professional-DJ-Software` | lure_repo |
| url | `https://github.com/MinotaurByteBond10/Twinmotion-2026-Free-Professional-Architectural-Visualization` | lure_repo |
| url | `https://github.com/SkyGeomancer/Chaos-V-Ray-Collection-Free-Professional-3D-Rendering` | lure_repo |
| url | `https://github.com/Galaxyeitriumph/Graphisoft-Archicad-29-Collaborate-Free-Professional-BIM-Design` | lure_repo |
| url | `https://github.com/spirebossrescue/D5-Render-Teams-3.1.1-Free-Professional-3D-Rendering` | lure_repo |
| url | `https://github.com/SheetMythStretch/Vectorworks-Architect-2027-Free-Professional-BIM-Design` | lure_repo |
| url | `https://github.com/existenceblazecanyon/SOLIDWORKS-Design-Ultimate-2026-Free-Professional-3D-CAD` | lure_repo |
| url | `https://github.com/LavaDeerHook/Autodesk-Inventor-Professional-2027-Free-3D-CAD-Design` | lure_repo |
| url | `https://github.com/AnalystSucceed/HWID-Testing-Utility-Free-Hardware-ID-Management` | lure_repo |
| url | `https://github.com/CoalSmokeMake/voicemod` | lure_repo |
| url | `https://github.com/PulverizeFrogFigure/voicemod` | lure_repo |
| url | `https://github.com/FloodChemistQuilt/voicemod` | lure_repo |
| url | `https://github.com/cliffmotormanvolt38/winutilits` | lure_repo |
| url | `https://github.com/PeakEconomicFetter/Filmora16-Ai-Editor-Plus` | lure_repo |
| url | `https://github.com/limetempodemodulator/Microsoft-Power-BI-Pro` | lure_repo |
| url | `https://github.com/ColorsSwanFlare/After-Effects` | lure_repo |
| url | `https://github.com/AreaCounselorFurnace/EaseUS-Todo-Backup` | lure_repo |
| url | `https://github.com/ForestBladesmith/Adobe-Audition-PC` | lure_repo |
| url | `https://github.com/Modernlavilla/GTA6-PC` | lure_repo |
| url | `https://github.com/SolarMistSay/REAPER-7.84-Free-Professional-Audio-Production` | lure_repo |
| url | `https://github.com/beatlarkknow/Foundry-Nuke-Studio-Free-Download-VFX-Software` | lure_repo |
| url | `https://github.com/Entityoverregister/FL-Studio-Free-Download-Modified-Edition` | lure_repo |
| url | `https://github.com/creekspiderwrench/Neat-Video-Professional-Video-Noise-Reduction` | lure_repo |
| url | `https://github.com/marblecashierdeflate/Adobe-After-Effects-Modified-Edition` | lure_repo |
| url | `https://github.com/SoundCourier/Steinberg-Cubase-Music-Production-Software` | lure_repo |
| url | `https://github.com/Sandglodepot35/Boris-FX-Suite-VFX-Motion-Graphics` | lure_repo |
| url | `https://github.com/RetroDukeGrasp/CapCut-Pro-Advanced-Video-Editing-Software` | lure_repo |
| url | `https://github.com/Goliathvubarrier/VEGAS-Pro-Professional-Video-Editing-Software` | lure_repo |
| url | `https://github.com/AttorneyPrime/DVDFab-Enlarger-AI-Free-AI-Video-Upscaling` | lure_repo |
| url | `https://github.com/Celestialdenlure/DaVinci-Resolve-Studio-Video-Editing-Color-Grading` | lure_repo |
| url | `https://github.com/beingtyrantdescribe/Wondershare-Filmora-Premium-Video-Editing-Software` | lure_repo |
| url | `https://github.com/LovebirdQuest/Mocha-Pro-Free-Download-Motion-Tracking-VFX` | lure_repo |
| url | `https://github.com/SpikeEmissary/Avid-Pro-Tools-Ultimate-Free-Professional-Audio-Production` | lure_repo |
| url | `https://github.com/HighwayPixel/Avid-Media-Composer-Professional-Video-Editing` | lure_repo |
| url | `https://github.com/SageSpanner84/Cavalry-Free-2D-Animation-Motion-Graphics-Software` | lure_repo |
| url | `https://github.com/GlazeFighter9/Maschine-3-Bundle-Free-Beat-Making-Music-Production` | lure_repo |
| url | `https://github.com/opencolonelswell/Bitwig-Studio-6-Free-Professional-Music-Production` | lure_repo |
| url | `https://github.com/Capturebrifence/Adobe-Audition-26.5-Professional-Audio-Editing` | lure_repo |
| url | `https://github.com/ChauffeurMoon91/FilmLight-Baselight-v7-Free-Professional-Color-Grading` | lure_repo |
| url | `https://github.com/PanelLocksmithSquare/Blackmagic-Fusion-Studio-21-Free-Professional-VFX` | lure_repo |
| url | `https://github.com/handcuffrajarepair/Adobe-Premiere-Pro-Free-Professional-Video-Editing` | lure_repo |
| url | `https://github.com/macrosergeantsquare/Native-Instruments-Massive-X-1.7-Free-Professional-Synthesizer` | lure_repo |
| url | `https://github.com/RealRegionKind/iZotope-Ozone-12-Advanced-Free-Professional-Audio-Mastering` | lure_repo |
| url | `https://github.com/Psycheoftrim36/Spitfire-Audio-BBC-Symphony-Orchestra-Professional-Free` | lure_repo |
| url | `https://github.com/Torrentdreinferno/EastWest-ComposerCloud-Free-Premium-Virtual-Instruments` | lure_repo |
| url | `https://github.com/Slowgrerhythm/Xfer-Serum-2-Free-Professional-Wavetable-Synthesizer` | lure_repo |
| url | `https://github.com/LusterJouninAtone25/Spectrasonics-Omnisphere-3-Free-Professional-Synthesizer` | lure_repo |
| url | `https://github.com/BreezeFlamingoGorge/Sound-Forge-Plus-2026-Free-Professional-Audio-Editing` | lure_repo |
| url | `https://github.com/ComponentSupplier/Waves-Ultimate-V17-Free-Professional-Audio-Plugins` | lure_repo |
| url | `https://github.com/dreamcyclevoyage/Plugin-Alliance-PRO-Free-Professional-Audio-Plugins` | lure_repo |
| url | `https://github.com/RouteShelter/Arturia-Pigments-7-Free-Professional-Synthesizer` | lure_repo |
| url | `https://github.com/Shellfespiral/Native-Instruments-Kontakt-8-Full-Free-Professional-Sampler` | lure_repo |
| url | `https://github.com/PointAirRecover56/Wise-Care` | lure_repo |
| url | `https://github.com/Rhythmtrualter/Wise-Registrity` | lure_repo |
| url | `https://github.com/silverindustrialgap/Auslogics` | lure_repo |
| url | `https://github.com/RopemakerCoil/Burning-Studio` | lure_repo |
| url | `https://github.com/sandsheriffbeat/Cinebench` | lure_repo |
| url | `https://github.com/SegmentWarden/Data-Grip` | lure_repo |
| url | `https://github.com/squareswimmeryell/Easy-Worship` | lure_repo |
| url | `https://github.com/SplendorCooper/ExitLag` | lure_repo |
| url | `https://github.com/StylistMultiplexer/HitFilm` | lure_repo |
| url | `https://github.com/symboladvocateshaft/KeyShot-Pro` | lure_repo |
| url | `https://github.com/VaultAssurance/PHP-Storm` | lure_repo |
| url | `https://github.com/wellflashalter/RX-11-Audio-Editor` | lure_repo |
| url | `https://github.com/vortexlakecanal/Rufus` | lure_repo |
| url | `https://github.com/Wyrmfosafeguard/Sylenth-1` | lure_repo |
| url | `https://github.com/yarnvoicedesignate/ultra-Iso` | lure_repo |
| url | `https://github.com/MediatorRevive/CCleaner-Pro` | lure_repo |
| url | `https://github.com/Attodreslicer/drphone-data-recovery` | lure_repo |
| url | `https://github.com/56411952/aion-2-enhancement-suite` | lure_repo |
| url | `https://github.com/foursixity001-hub/aion-2-enhancement-suite` | lure_repo |
| url | `https://github.com/joaopedro903/delta-executor-desktop-toolkit` | lure_repo |
| url | `https://github.com/GpiceQ/inventor-desktop-installer` | lure_repo |
| url | `https://github.com/Hubkrereanimate/Secure-PDF-Workstation` | lure_repo |
| url | `https://github.com/Omegaofidolize/ableton-live-12` | lure_repo |
| url | `https://github.com/phantomsociallook/auslogics` | lure_repo |
| url | `https://github.com/Pointyodemolish/bloxshade-for-roblox` | lure_repo |
| url | `https://github.com/PlanetCraneInterface/autodesk-revit` | lure_repo |
| url | `https://github.com/platooncaptainmarket/better-discord` | lure_repo |
| url | `https://github.com/QuakeAdmiral/crash-plan` | lure_repo |
| url | `https://github.com/ShackleCosmetologist/genesis-scanner` | lure_repo |
| url | `https://github.com/shalecorporatelabel/grayket` | lure_repo |
| url | `https://github.com/SmokeObliterate/imyfone` | lure_repo |
| url | `https://github.com/SphereMagistrate39/metatrader` | lure_repo |
| url | `https://github.com/TerminusPotter/quant-trading-bot` | lure_repo |
| url | `https://github.com/VillageExecutive/ultra-edit` | lure_repo |
| url | `https://github.com/VolcanoBaseCock/voicechanger` | lure_repo |
| url | `https://github.com/WeaponsmithPray/winutilits` | lure_repo |
| url | `https://github.com/WeaveSeekerJinx/wise-care` | lure_repo |
| url | `https://github.com/Falsetervitalize/discord-server-raider` | lure_repo |
| url | `https://github.com/gripdiplomatendure1/melodyne-5` | lure_repo |
| url | `https://github.com/gryphonduckdefend/microsoft-office` | lure_repo |
| url | `https://github.com/Grottoflachain/microsoft-365` | lure_repo |
| url | `https://github.com/hopegiraffestride/movavi-video-editor-plus` | lure_repo |
| url | `https://github.com/JumperCrater/pump-fun` | lure_repo |
| url | `https://github.com/MechanicClaim/total-commander` | lure_repo |
| url | `https://github.com/mortalswanstrait/wise-care` | lure_repo |
| url | `https://github.com/DeimosPhobos666/office-suite-validator` | lure_repo |
| url | `https://github.com/rimoharp/melodyne-5` | lure_repo |
| domain | `ps-ps.cc` | lure_delivery_domain |
| domain | `git-software.cc` | lure_delivery_domain |
| domain | `quickrun31.cc` | lure_delivery_domain |
| domain | `appget29.tools` | lure_delivery_domain |
| domain | `log.travelvault.today` | stealer_c2 |
| url | `https://telegra.ph/Canvas-grove-11-19` | dead_drop |
| contract_address | `0x45a7B8fAec623508bd68be535Cc7618f283ddB48` | resolver_contract |
| url | `https://github.com/Unitphisignify/xswodvro` | lure_repo |
| url | `https://github.com/driftcuttlefishjump/Serato-DJ-Pro` | lure_repo |
| url | `https://github.com/armorsurgeonstill7/Clion` | lure_repo |
| url | `https://github.com/PlotOtokageRespect/GrayKet` | lure_repo |
| url | `https://github.com/ceilingforemanrank/CapCut-for-Windows` | lure_repo |
| url | `https://github.com/BowyerSqueeze/Avid-Media-Composer` | lure_repo |
| url | `https://github.com/fuserainday80/AOMEI-Backupper` | lure_repo |
| url | `https://github.com/Sandstonetenoutfit/Cinebench` | lure_repo |
| url | `https://github.com/Crestchadome/VoiceChanger` | lure_repo |
| url | `https://github.com/Ninjaclaplunder36/AnyDesk` | lure_repo |
| url | `https://github.com/rainfrogrectifier41/Avid-Media-Composer` | lure_repo |
| url | `https://github.com/rainfrogrectifier41/Autodesk-3ds-MAX` | lure_repo |
| url | `https://github.com/LimestoneCaptain/FabFilter-Total` | lure_repo |
| url | `https://github.com/PinkTrackDesignate/Movavi-Video-Editor-Plus` | lure_repo |
| url | `https://github.com/ApparitionElkCorrect/Wise-Care` | lure_repo |
| url | `https://github.com/Colorstoserver/Movavi-Effects` | lure_repo |
| url | `https://github.com/ShopkeeperConnector/Wise-Registrity` | lure_repo |
| url | `https://github.com/frostaxetrough/Designcenter-NX` | lure_repo |
| url | `https://github.com/WraithTellerSpout/Autodesk-3ds-MAX` | lure_repo |
| url | `https://github.com/LevelSparkRecognize/Ashampoo-WinOptimizer` | lure_repo |
| url | `https://github.com/Flashbylevel/FabFilter-Pro` | lure_repo |
| url | `https://github.com/BlueProvostCrush/Quicken-Deluxe` | lure_repo |
| url | `https://github.com/Volumetheboutique/Directory-Opus` | lure_repo |
| url | `https://github.com/ViceAdvocate/ArchiCAD` | lure_repo |
| url | `https://github.com/MajorShaperCultivate/Acronis` | lure_repo |
| url | `https://github.com/MajorShaperCultivate/Ableton-Live-12` | lure_repo |
| url | `https://github.com/BottomHeronEradicate/Movavi-Screen-Recorder` | lure_repo |
| url | `https://github.com/FollowerPruner/Melodyne-5` | lure_repo |
| url | `https://github.com/UnicornShade/PHP-Storm` | lure_repo |
| url | `https://github.com/Demonsemarvel/Auslogics` | lure_repo |
| url | `https://github.com/Icechiponder/SoundPad` | lure_repo |
| url | `https://github.com/MortalGoldsmith40/Autodesk-Revit` | lure_repo |
| url | `https://github.com/Topunderfeel/Ableton-Live-12` | lure_repo |
| url | `https://github.com/Topunderfeel/Acronis` | lure_repo |
| url | `https://github.com/StoneParakeet/Movavi-Video-Suite-Plus` | lure_repo |
| url | `https://github.com/EastShipperRestore/SonyVegas` | lure_repo |
| url | `https://github.com/beastofficerfollow/Movavi-Photo-Editor` | lure_repo |
| url | `https://github.com/LizardScissors/Adobe-Acrobat-Pro` | lure_repo |
| url | `https://github.com/metropolisorioletap/Adobe-InDesign` | lure_repo |
| url | `https://github.com/metropolisorioletap/Actual-Multiplie-Monitors` | lure_repo |
| url | `https://github.com/Lineureliminate/HitFilm` | lure_repo |
| url | `https://github.com/PillarStreamPipe/Burning-Studio` | lure_repo |
| url | `https://github.com/Matterwithinbastion/Data-Grip` | lure_repo |
| url | `https://github.com/GaleVeterinarian/Power-Director` | lure_repo |
| url | `https://github.com/DimCommercialFactory/Start11` | lure_repo |
| url | `https://github.com/GlueRealmProduce/Cellebrite-UFED` | lure_repo |
| url | `https://github.com/EmirOvercome/Adobe-After-Effects` | lure_repo |
| url | `https://github.com/MagicArbiter/Easy-Worship` | lure_repo |
| url | `https://github.com/PersonalityWalker/Movavi-Converter` | lure_repo |
| url | `https://github.com/AdmiralDiscriminate/Photo-Commander` | lure_repo |
| url | `https://github.com/holeconductorcrush/Kontakt-8` | lure_repo |
| url | `https://github.com/hubdragonminaret/VoiceMod` | lure_repo |
| url | `https://github.com/Windaurotation/Canva-Pro` | lure_repo |
| url | `https://github.com/Windaurotation/Better-Discord` | lure_repo |
| url | `https://github.com/Capitalaosteeple24/sbzjbgdy` | lure_repo |
| url | `https://github.com/kindguruboost/Data-Grip` | lure_repo |
| url | `https://github.com/HiddenSparrowMinaret/Wise-Registrity` | lure_repo |
| url | `https://github.com/FoalShrink50/Movavi-Effects` | lure_repo |
| url | `https://github.com/Weavebennurture/Burning-Studio` | lure_repo |
| url | `https://github.com/Weavebennurture/Avid-Media-Composer` | lure_repo |
| url | `https://github.com/Lineinmonitor/Ozone-12-Advanced` | lure_repo |
| url | `https://github.com/PortionHelmsman/Movavi-Converter` | lure_repo |
| url | `https://github.com/ashcustodiandolmen/Cinebench` | lure_repo |
| url | `https://github.com/TrackViceCraft/Movavi-Video-Editor-Plus` | lure_repo |
| url | `https://github.com/BayAssociate/Directory-Opus` | lure_repo |
| url | `https://github.com/sharpbytekey/Movavi-Video-Suite-Plus` | lure_repo |
| url | `https://github.com/SavageSamuraiTuck/CorelDraw` | lure_repo |
| url | `https://github.com/PeltPythonCall/GrayKet` | lure_repo |
| url | `https://github.com/Griffinlyatreasure85/Cellebrite-UFED` | lure_repo |
| url | `https://github.com/Thornonanchorage/Ashampoo-WinOptimizer` | lure_repo |
| url | `https://github.com/MarshalTrench/SonyVegas` | lure_repo |
| url | `https://github.com/snatchbytesalvage/CCleaner-Pro` | lure_repo |
| url | `https://github.com/SaboteurClip/Rufus` | lure_repo |
| url | `https://github.com/JoinBardColonnade/RX-11-Audio-Editor` | lure_repo |
| url | `https://github.com/PlanetPhaseRaid/VoiceMod` | lure_repo |
| url | `https://github.com/Openbygather/Movavi-Photo-Editor` | lure_repo |
| url | `https://github.com/ScrewDiverHike/Power-Director` | lure_repo |
| url | `https://github.com/Ratiokrunote/Movavi-Converter` | lure_repo |
| url | `https://github.com/SlateElementalist/SystemCare-Pro` | lure_repo |
| url | `https://github.com/Minotaurtruflex/Microsoft-Project` | lure_repo |
| url | `https://github.com/MelodySwimmer/Ultra-Edit` | lure_repo |
| url | `https://github.com/Openyodepict/Movavi-Video-Editor-Plus` | lure_repo |
| url | `https://github.com/EssenceConductor/Movavi-Video-Suite-Plus` | lure_repo |
| url | `https://github.com/crimsonoriolehovel/Movavi-Effects` | lure_repo |
| url | `https://github.com/HornbillJournal/Photo-Commander` | lure_repo |
| url | `https://github.com/TarantulaKnow/Movavi-Screen-Recorder` | lure_repo |
| url | `https://github.com/StreetGateChisel/Uttorent` | lure_repo |
| url | `https://github.com/PathTailorRadial/StartAll-Back` | lure_repo |
| url | `https://github.com/portalthunderphase/Movavi-Photo-Editor` | lure_repo |
| url | `https://github.com/ExistenceProduction/Auslogics` | lure_repo |
| url | `https://github.com/PaintShrimpDawn/Canva-Pro` | lure_repo |
| url | `https://github.com/MailJudgeView/SoundPad` | lure_repo |
| url | `https://github.com/Ponddergenerate/Movavi-Video-Suite-Plus` | lure_repo |
| url | `https://github.com/ChainWizardAura/Cinebench` | lure_repo |
| url | `https://github.com/SmartThunderDisplay/Movavi-Screen-Recorder` | lure_repo |
| url | `https://github.com/FlowBeetle94/Autodesk-Revit` | lure_repo |
| url | `https://github.com/Towerthroughlabel/FabFilter-Total` | lure_repo |
| url | `https://github.com/BlacksmithColumn/AOMEI-Backupper` | lure_repo |
| url | `https://github.com/FaceDuckStove/CapCut-for-Windows` | lure_repo |
| url | `https://github.com/ringorcastay/Ashampoo-WinOptimizer` | lure_repo |
| url | `https://github.com/SerpentCleric/Uttorent` | lure_repo |
| url | `https://github.com/volumesamuraichill/SystemCare-Pro` | lure_repo |
| url | `https://github.com/NightBiomancer/Cellebrite-UFED` | lure_repo |
| url | `https://github.com/Grandmasterofend/Melodyne-5` | lure_repo |
| url | `https://github.com/mudcoxswainpit/Movavi-Converter` | lure_repo |
| url | `https://github.com/GiraffeCondense/Burning-Studio` | lure_repo |
| url | `https://github.com/ShoreRealm72/RX-11-Audio-Editor` | lure_repo |
| url | `https://github.com/WharfStarHike/Wise-Registrity` | lure_repo |
| url | `https://github.com/BladesmithFirewall/KeyShot-Pro` | lure_repo |
| url | `https://github.com/GraphLoopGame/FabFilter-Pro` | lure_repo |
| url | `https://github.com/DragonHokageDecoder/Total-Commander` | lure_repo |
| url | `https://github.com/Tracksiawning/VoiceMod` | lure_repo |
| url | `https://github.com/chaindictatorpalace/AnyDesk` | lure_repo |
| url | `https://github.com/Obsidiangrohoist/HitFilm` | lure_repo |
| url | `https://github.com/Ditcharbarrier/ExitLag` | lure_repo |
| url | `https://github.com/FigureNetworkConsole/Movavi-Video-Editor-Plus` | lure_repo |
| url | `https://github.com/FenceSpinnerGuide/Rufus` | lure_repo |
| url | `https://github.com/bittsuchikagelaud/Avid-Media-Composer` | lure_repo |
| url | `https://github.com/Earthyodeliver16/Power-Director` | lure_repo |
| url | `https://github.com/StreetMarine/Autodesk-3ds-MAX` | lure_repo |
| url | `https://github.com/FinalJourneyman/Movavi-Effects` | lure_repo |
| url | `https://github.com/megasheriffswell/Photo-Commander` | lure_repo |
| url | `https://github.com/ClawFollowerMall/Chief-Architect-Premier` | lure_repo |
| url | `https://github.com/torrentclassbay/SonyVegas` | lure_repo |
| url | `https://github.com/oillovebirdbuild/Total-Commander` | lure_repo |
| url | `https://github.com/ProviderRelease64/WinUtilits` | lure_repo |
| url | `https://github.com/pentagongeneralgaze/VoiceChanger` | lure_repo |
| url | `https://github.com/PheasantMetro/Uttorent` | lure_repo |
| url | `https://github.com/opticantbarrow/Ultra-Edit` | lure_repo |
| url | `https://github.com/silverofficialdusk/Easeus-Todo-Backup-For-Windows` | lure_repo |
| url | `https://github.com/sparkfiremancollar21/Microsoft-Project-For-Windows` | lure_repo |
| url | `https://github.com/BetaChampionTitle/Coreldraw-For-Windows` | lure_repo |
| url | `https://github.com/StitchSerfJump/Microsoft-Visio-For-Windows` | lure_repo |
| url | `https://github.com/DeckhandIgnite/Davinci-Resolve-Studio-For-Windows` | lure_repo |
| url | `https://github.com/ElementalistTurbine/Ccleaner-Professional-For-Windows` | lure_repo |
| url | `https://github.com/MudTsuchikage/Fl-Studio-For-Windows` | lure_repo |
| url | `https://github.com/OrangeSaviorImagine/Abbyy-Finereader-Pdf-For-Windows` | lure_repo |
| url | `https://github.com/Velocityatrhythm/Autodesk-3ds-Max-For-Windows` | lure_repo |
| url | `https://github.com/MortarBeetleStyle/Autocad-For-Windows` | lure_repo |
| url | `https://github.com/CatchArtisanDone86/Movavi-Video-Editor-For-Windows` | lure_repo |
| url | `https://github.com/Sandsisupervise20/Adobe-Premiere-Pro-For-Windows-And-Macos` | lure_repo |
| url | `https://github.com/gleameconomicjetty/Adobe-Indesign-For-Windows-And-Macos` | lure_repo |
| url | `https://github.com/ManeSwordGraph/Adobe-Lightroom-Classic-For-Windows-And-Macos` | lure_repo |
| url | `https://github.com/Cachewithinmake/GTA6-Preload-PC` | lure_repo |
| url | `https://github.com/SageAdapter8/Rob-Run-Mod-Menu` | lure_repo |
| url | `https://github.com/Weavedrobless13/Actual-Multiplie-Monitors` | lure_repo |
| url | `https://github.com/Weavedrobless13/Acronis` | lure_repo |
| url | `https://github.com/Wireearadial/Adobe-After-Effects` | lure_repo |
| url | `https://github.com/Wireearadial/Actual-Multiplie-Monitors` | lure_repo |
| url | `https://github.com/WharfBeetleGallery37/Acronis` | lure_repo |
| url | `https://github.com/WharfBeetleGallery37/Ableton-Live-12` | lure_repo |
| url | `https://github.com/ShaleNurseBurst/Wise-Registrity` | lure_repo |
| url | `https://github.com/ManufacturingTurbine/Serato-DJ-Pro` | lure_repo |
| url | `https://github.com/BondFletcher/Ashampoo-WinOptimizer` | lure_repo |
| url | `https://github.com/angleartisanstitch/SystemCare-Pro` | lure_repo |
| url | `https://github.com/JoinDamselReduce/Movavi-Video-Suite-Plus` | lure_repo |
| url | `https://github.com/beastcrewmanraise56/AutoCad` | lure_repo |
| url | `https://github.com/CaptainFurnish/AOMEI-Backupper` | lure_repo |
| url | `https://github.com/celestialsteamsupply/Movavi-Video-Suite-Plus` | lure_repo |
| url | `https://github.com/PathSwallowLock/Wise-Care` | lure_repo |
| url | `https://github.com/BrokerSpiral/CapCut-for-Windows` | lure_repo |
| url | `https://github.com/convergeattorneyquay/Claude-Jailbreak-Prompt` | lure_repo |
| url | `https://github.com/Holeyospindle/Movavi-Effects` | lure_repo |
| url | `https://github.com/Polygonglicavity/FL-Studio` | lure_repo |
| url | `https://github.com/Sandstonelunamode/Autodesk-Revit` | lure_repo |
| url | `https://github.com/MatrixSeaCode25/SketchUp-Pro` | lure_repo |
| url | `https://github.com/HarborAxolotl/Kontakt-8` | lure_repo |
| url | `https://github.com/StoragePupaAgitate/CorelDraw` | lure_repo |
| url | `https://github.com/Magicvanmemorialize/Quicken-Deluxe` | lure_repo |
| url | `https://github.com/OfficialHook/VoiceChanger` | lure_repo |
| url | `https://github.com/NoviceBandage/Ashampoo-Uninstaller` | lure_repo |
| url | `https://github.com/TrapSilversmith/KeyShot-Pro` | lure_repo |
| url | `https://github.com/beamcrystalplunder/Actual-Multiplie-Monitors` | lure_repo |
| url | `https://github.com/CassowaryMansion/Autodesk-CFD` | lure_repo |
| url | `https://github.com/BadgeHealerConverter/Adobe-After-Effects` | lure_repo |
| url | `https://github.com/Fabledandtrowel/Claude-Jailbreak-Prompt` | lure_repo |
| url | `https://github.com/ExaMajorYell/FabFilter-Pro` | lure_repo |
| url | `https://github.com/SphereIguana8/AutoCad` | lure_repo |
| url | `https://github.com/legendaryturkeyspark/Ozone-12-Advanced` | lure_repo |
| url | `https://github.com/azurepikemandivide/GrayKet` | lure_repo |
| url | `https://github.com/GraphSoldierPergola/Instagram-Liker-Bot` | lure_repo |
| url | `https://github.com/DensityCooper/Designcenter-NX` | lure_repo |
| url | `https://github.com/FlowScorpion/HitFilm` | lure_repo |
| url | `https://github.com/Feelingubattle/FL-Studio` | lure_repo |
| url | `https://github.com/Characternearequip/CCleaner-Pro` | lure_repo |
| url | `https://github.com/mintconductorzen/SonyVegas` | lure_repo |
| url | `https://github.com/colonylightsever/Cinebench` | lure_repo |
| url | `https://github.com/bodyconquerorclimb/Adobe-Substance-3d` | lure_repo |
| url | `https://github.com/heightsongsouk/Microsoft-365` | lure_repo |
| url | `https://github.com/Cacheacrossregain/Auslogics` | lure_repo |
| url | `https://github.com/phantombudgiesheave/Wise-Registrity` | lure_repo |
| url | `https://github.com/Arenadensocket/Data-Grip` | lure_repo |
| url | `https://github.com/ChampionHaulerFlue/Burning-Studio` | lure_repo |
| url | `https://github.com/Ensignchetrap/Easy-Worship` | lure_repo |
| url | `https://github.com/NightingaleHinge/CCleaner-Pro` | lure_repo |
| url | `https://github.com/FabledEmpressFree19/FabFilter-Total` | lure_repo |
| url | `https://github.com/Coaliocontact/Chief-Architect-Premier` | lure_repo |
| url | `https://github.com/hornsurgeontweezers/Movavi-Converter` | lure_repo |
| url | `https://github.com/anglemayorwinch30/ArchiCAD` | lure_repo |
| url | `https://github.com/Topazchosouk/Autodesk-Inventor` | lure_repo |
| url | `https://github.com/BarbTernCrack/Acronis` | lure_repo |
| url | `https://github.com/wyrmlawyerberth/Catia-Cad` | lure_repo |
| url | `https://github.com/Highwayphomoon/Microsoft-Visio` | lure_repo |
| url | `https://github.com/Dockuafill99/Directory-Opus` | lure_repo |
| url | `https://github.com/BeamHornetStation/Adobe-Photoshop` | lure_repo |
| url | `https://github.com/OceanViceIgnite97/Cinebench` | lure_repo |
| url | `https://github.com/DustInterest/Ashampoo-WinOptimizer` | lure_repo |
| url | `https://github.com/Captureglewharf/Autodesk-Inventor` | lure_repo |
| url | `https://github.com/stratumvaporrecall/Melodyne-5` | lure_repo |
| url | `https://github.com/OperativeNegotiator/WinUtilits` | lure_repo |
| url | `https://github.com/Ambereuform65/Adobe-Acrobat-Pro` | lure_repo |
| url | `https://github.com/MagentaMonetary/PHP-Storm` | lure_repo |
| url | `https://github.com/Stuccoflarear/Burning-Studio` | lure_repo |
| url | `https://github.com/GraspEmissaryKiln/Ads-Blocker` | lure_repo |
| url | `https://github.com/Mortalveamend/StartAll-Back` | lure_repo |
| url | `https://github.com/cascadefireflychill/Instagram-Liker-Bot` | lure_repo |
| url | `https://github.com/DecaStudentIncrease/Data-Grip` | lure_repo |
| url | `https://github.com/GripEmuSupply/FabFilter-Total` | lure_repo |
| url | `https://github.com/MarineBridge/RX-11-Audio-Editor` | lure_repo |
| url | `https://github.com/Centisaintpuzzle/Autodesk-Revit` | lure_repo |
| url | `https://github.com/TheaterOcean/ExitLag` | lure_repo |
| url | `https://github.com/beattestingdisplay/Directory-Opus` | lure_repo |
| url | `https://github.com/CenterBorder/Imei-Repair` | lure_repo |
| url | `https://github.com/Hidefitzoscillate/Microsoft-Project` | lure_repo |
| url | `https://github.com/HectoGoldsmith/Melodyne-5` | lure_repo |
| url | `https://github.com/Copperrutrim/AnyUnlock` | lure_repo |
| url | `https://github.com/beachactivistmanor/Adobe-Audition` | lure_repo |
| url | `https://github.com/tunnelowlcutters/Display-Fusion` | lure_repo |
| url | `https://github.com/TrueSkyTassel/Auslogics` | lure_repo |
| url | `https://github.com/flattoucanphase/GrayKet` | lure_repo |
| url | `https://github.com/CommercialRuminate/Autodesk-CFD` | lure_repo |
| url | `https://github.com/PurpleStationCharge/AnyDesk` | lure_repo |
| url | `https://github.com/exajackdawmall/ExitLag` | lure_repo |
| url | `https://github.com/LimestoneTellerHover/Serato-DJ-Pro` | lure_repo |
| url | `https://github.com/BasiliskBrakemanMoon/ArchiCAD` | lure_repo |
| url | `https://github.com/barrierpilotcatalog/Ads-Blocker` | lure_repo |
| url | `https://github.com/NodeRajaCrater/Cellebrite-UFED` | lure_repo |
| url | `https://github.com/trueparakeetadmire63/AOMEI-Backupper` | lure_repo |
| url | `https://github.com/NinjaLynxFlow/SystemCare-Pro` | lure_repo |
| url | `https://github.com/VectorMotorman/Clion` | lure_repo |
| url | `https://github.com/monsterroguecontinue/Start11` | lure_repo |
| url | `https://github.com/Monstereuraise/Audition-Pc` | lure_repo |
| url | `https://github.com/WraithSheikh/stellar-recovery-hard-disk` | lure_repo |
| url | `https://github.com/FuseVanquisher/dex-screener-crypto-analytics` | lure_repo |
| url | `https://github.com/GhostMeadowlark/EaseUS-Todo-Backup` | lure_repo |
| url | `https://github.com/WeightAlbatross/Uipath-Studio` | lure_repo |
| url | `https://github.com/LoopPresident/aion-2-bot-auto-farm-optimizer` | lure_repo |
| url | `https://github.com/Portionshuupgrade/wardogs-cheat-game-trainer` | lure_repo |
| url | `https://github.com/leveetempoemancipate/Power-Bio-PC-Full` | lure_repo |
| url | `https://github.com/GlowPolitician/rust-scripts-automation-tools` | lure_repo |
| url | `https://github.com/Tabooonchain/slay-the-spire-2-mods` | lure_repo |
| url | `https://github.com/LookoutVisionRivet/path-of-exile-2-bot` | lure_repo |
| url | `https://github.com/momentumtiername/-xsplit-broadcaster` | lure_repo |
| url | `https://github.com/PharaohManage/construct3` | lure_repo |
| url | `https://github.com/PinTechnicianBang/ets2-mods-trainer` | lure_repo |
| url | `https://github.com/PhysicianDominate/marvel-rivals-skin-changer-tools` | lure_repo |
| url | `https://github.com/gridloaderrepair/Vmix-Pro` | lure_repo |
| url | `https://github.com/TremorRider54/FMOD-Studio` | lure_repo |
| url | `https://github.com/SpikeAxolotl/FL-STUDIO-PC` | lure_repo |
| url | `https://github.com/BeetleRemain/gta-6-pc-download` | lure_repo |
| domain | `pkgsetup.cc` | lure_delivery_domain |
| url | `https://github.com/BehemothDyer/stable-diffusion-atelier` | lure_repo |
| url | `https://github.com/Brinkoversteeple/docker-compose-stash` | lure_repo |
| url | `https://github.com/EmissaryHike/jellyfin-media-notebook` | lure_repo |
| url | `https://github.com/Glosszumlattice/quickbooks-ledger-alts` | lure_repo |
| url | `https://github.com/Hubarsalvage/nintendo-switch-emulation-desk` | lure_repo |
| url | `https://github.com/OutpostPython/tableau-viz-gallery` | lure_repo |
| url | `https://github.com/Tensorflearcade/ps5-backup-saver` | lure_repo |
| url | `https://github.com/VendorShelter/telegram-bot-foundry` | lure_repo |
| url | `https://github.com/VillagePrefect/stable-diffusion-atelier` | lure_repo |
| url | `https://github.com/WindServiceIdentify/ableton-production-bench` | lure_repo |
| url | `https://github.com/grottosanninvoyage/k8s-homelab-sailor` | lure_repo |
| url | `https://github.com/nora-herrera49/ADlabs-toolz` | lure_repo |
| url | `https://github.com/polygondomainport/obs-streamer-stack` | lure_repo |
| url | `https://github.com/silverbeatcompute/jellyfin-media-notebook` | lure_repo |
| url | `https://github.com/superstormfringe/autohotkey-trove` | lure_repo |
| url | `https://github.com/KrakenCraneCraft/Wirecast-Version-Pro` | lure_repo |
| url | `https://github.com/ProsecutorSpade/Premier-Version-Pro` | lure_repo |
| url | `https://github.com/Woodglodisclose/DXO-PHOTOLAB-10-ELITE` | lure_repo |
| url | `https://github.com/TrenchZebraMaster/Capture-One-Pro` | lure_repo |
| url | `https://github.com/Streetthetent33/Avid-Pro-Tools-Ultimate` | lure_repo |
| url | `https://github.com/trapworkerravine/Davinci-resolve-version-pro` | lure_repo |
| url | `https://github.com/WildCooperYank/vMix-Pro` | lure_repo |
| url | `https://github.com/LogoGunsmithSteeple/siemens-nx-full-version` | lure_repo |
| url | `https://github.com/onyxformvise/Autodesk-Revit-Full-Version` | lure_repo |
| url | `https://github.com/SeniorExemplify/Adobe-Illustrator-Full-Version` | lure_repo |
| url | `https://github.com/CorporateAxle/Steinberg-Nuendo-Full-version` | lure_repo |
| url | `https://github.com/protonemuseparator/catia-3dexperience-full-version` | lure_repo |
| url | `https://github.com/SpeedGiraffeWatt96/CorelDRAW-Graphics-Suite` | lure_repo |
| url | `https://github.com/Followerpuvault/Autodesk-AutoCAD-Full-Version` | lure_repo |
| url | `https://github.com/Matrixacrosscompact/SideFX-Houdini-FX-Full-Version` | lure_repo |
| url | `https://github.com/ViceDeveloper/ivcam-full-version` | lure_repo |
| url | `https://github.com/AmbassadorHonor/Autodesk-Maya-Full-Version` | lure_repo |
| url | `https://github.com/Aquaunbungalow/Autodesk-3ds-max-full-version` | lure_repo |
| url | `https://github.com/Plumemccharge/Maxon-ZBrush-Full-Version` | lure_repo |
| url | `https://github.com/Watertrestring/camo-studio-pro-full-version` | lure_repo |
| url | `https://github.com/wildswiftintroduce/rob-run-mod-menu-zoel` | lure_repo |
| url | `https://github.com/GlossConstableShears/Unity-Pro-Full-Version` | lure_repo |
| url | `https://github.com/FloorHelmsmanAxle95/-Grand-Theft-Auto-VI-preload-pc` | lure_repo |
| url | `https://github.com/Modernuovacuum/gamemaker-professional-full-version` | lure_repo |
| url | `https://github.com/blazeclientvise/rob-run-tools` | lure_repo |
| url | `https://github.com/PeakNegotiatorKiln/Grand-Version-6` | lure_repo |

## Files

| SHA-256 |
| --- |
| `fbaeb724f58c6c90c38e1af9333b265dabe6e6f78509b47a21da9f9db0db23ec` |
| `75cae8dc8680c83a30588f24bfb2902071396117b8fd48a982f8ab8d031ecc9d` |
| `df3a3973900153a363e21385ca3394addac8d52c7547827dc334ebff75ee451b` |
| `9f293cda819b74342bb598291010ee02a96af71eb2dabc7ab4c94edea21afa9c` |
| `9974033ff14688dba81c1e48a8cf0d4237815ea4c185c8a09fe584812457b576` |
| `8a826a8d766d2fe7b0106e9435f319d8db02178a93a74cbdfa43c9094bf0c334` |
| `eef29c3207e463e789555d227c0aae4013cd0d457f80c157b7eb59dcce89ba6f` |
