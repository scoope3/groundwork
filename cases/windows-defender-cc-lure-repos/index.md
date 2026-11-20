# GitHub lure repos on aged batch-made accounts delivering an information stealer through pasted PowerShell commands

Category: infrastructure-setup-patterns  
Published: 2026-11-20  
Write-up: https://github.com/scoope3/groundwork/tree/main/cases/windows-defender-cc-lure-repos

## Summary

GitHub accounts created on a handful of days in June and August 2026 each got one empty repository and were then left alone. From 2026-10-18 those accounts began carrying a lure: a README dressed as a free, "pre-activated" copy of commercial software that tells the reader to paste one PowerShell line. On 2026-11-20, 110 of the 113 lure repositories known were live.

The pasted line downloads a loader script from one of five hosts. The loader downloads a password-protected RAR archive and an unpacker from `toolget2[.]lol`, unpacks it and starts the program inside. The chain was run end to end in a public Windows sandbox on Windows 10 and Windows 11.

The program is an information stealer with a download-and-run task feature. It exited within seconds in the sandbox. Its unpacked code was read statically: it checks for virtual machines, analysis tools and ten interface languages, and it is built to take browser data, wallets, password-manager and messenger data and developer secrets. It was never observed stealing anything. It decrypts its server address, `meta3[.]grovestack[.]one:443`, from a value built into the program, from a telegra[.]ph page and from a Polygon smart contract. The server was never contacted.

The contract was created by a wallet that has created 185 contracts of nearly identical size since 2026-10-08. That all of them are resolvers of this kind is an inference from their size and pattern; only two are tied to a malware build. A sibling build from the same download host was analysed first by Ethan Kawley ([Ethan-Ka/toolget2-malware-analysis](https://github.com/Ethan-Ka/toolget2-malware-analysis), 2026-11-03); its contract comes from the same wallet, and its server is listed below as his finding. Much of the reported behaviour overlaps Elastic Security Labs' description of REVSTEALER, with differences, and Elastic's detection rule does not match this sample, so the family is an inference.

## Reading the indicators

- `lure_delivery_domain`, `next_stage_host`, `stealer_c2`: hosts. Three of the delivery hosts are known only from README text; their scripts were never retrieved.
- `lure_repo`: the GitHub repositories carrying the lure, live when checked. They are evidence and a takedown list, not a claim about who owns the accounts.
- `dead_drop`, `resolver_contract`: a page on a public publishing service and a contract on a public blockchain. Block the specific page or watch for the specific call; do not block the services.
- `deployer_wallet`: kit scope. Whether the wallet belongs to one operator or to a service used by many is not known.
- `third_party_c2`: reported by another researcher and credited to him; not re-derived here.
- No first-finder claim is made for any indicator in this case.
- Files, in the order listed below: the loader script served at `devtools8[.]lol/j2sj9blzc` (PowerShell, 14,841 bytes, same hash in three sandbox runs); the loader script served at `monolit[.]sbs` (PowerShell, 4,819 bytes, retrieved 2026-11-18); the password-protected archive `67q65idtq.rar` served by `toolget2[.]lol` (3,286,078 bytes); and the stealer as delivered, `bh3xm14ke1.exe` (packed, self-signed, 3,460,200 bytes; hash reported by two analysis sessions). The unpacker the loader downloads is reported to be a genuine UnRAR build and is deliberately not listed.

Nothing in this case is attributed to a person or group.

## Evidence

| Evidence type | Scope | False-positive rate | On |
| --- | --- | --- | --- |
| dead_drop | operator | 0% | `https://telegra.ph/Clear-ridge-11-10` |
| deployer_wallet | kit | 0% | `0x8bAddf058D11005360900a0542484eE446F2d494` |
| lure_delivery_domain | operator | 0% | `windows-defender.cc` |
| lure_delivery_domain | operator | 0% | `monolit.sbs` |
| lure_delivery_domain | operator | 0% | `devtools8.lol` |
| lure_delivery_domain | operator | 0% | `power-shell.cc` |
| lure_delivery_domain | operator | 0% | `powershell.lat` |
| lure_delivery_domain | operator | 0% | `power-shell.cc` |
| lure_delivery_domain | operator | 0% | `monolit.sbs` |
| lure_delivery_domain | operator | 0% | `monolit.sbs` |
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
| lure_repo_template | kit | 0% | `github-repo-set:windows-defender-cc` |
| next_stage_host | operator | 0% | `toolget2.lol` |
| resolver_contract | operator | 0% | `0x1ee6A331881102B84d2DebdD5eefd2E591a65f14` |
| star_inflation_pattern | context | 0% | `github-account-batch:2026-08-10` |
| stealer_c2 | operator | 0% | `meta3.grovestack.one` |
| third_party_c2 | kit | 0% | `scheduler.echoform32.club` |

## Indicators

| Type | Indicator | Evidence | First finder |
| --- | --- | --- | --- |
| domain | `windows-defender.cc` | lure_delivery_domain | not claimed |
| domain | `monolit.sbs` | lure_delivery_domain | not claimed |
| domain | `devtools8.lol` | lure_delivery_domain | not claimed |
| domain | `toolget2.lol` | next_stage_host | not claimed |
| domain | `power-shell.cc` | lure_delivery_domain | not claimed |
| domain | `powershell.lat` | lure_delivery_domain | not claimed |
| domain | `meta3.grovestack.one` | stealer_c2 | not claimed |
| url | `https://telegra.ph/Clear-ridge-11-10` | dead_drop | not claimed |
| contract_address | `0x1ee6A331881102B84d2DebdD5eefd2E591a65f14` | resolver_contract | not claimed |
| crypto_address | `0x8bAddf058D11005360900a0542484eE446F2d494` | deployer_wallet | not claimed |
| domain | `scheduler.echoform32.club` | third_party_c2 | not claimed |
| url | `https://github.com/dreamtherapistcrypt/Chaos-Enscape-Collection-Free-Professional-3D-Rendering` | lure_repo | not claimed |
| url | `https://github.com/petacockatooblock/Chaos-Corona-Collection-Free-Professional-Architectural-Rendering` | lure_repo | not claimed |
| url | `https://github.com/Blizzardteawning/IK-Multimedia-AmpliTube-5-MAX-v2-Free-Guitar-Bass-Modeling` | lure_repo | not claimed |
| url | `https://github.com/Pondshoreproduce/Celemony-Melodyne-5-Studio-Free-Professional-Vocal-Tuning` | lure_repo | not claimed |
| url | `https://github.com/Scalarbatturn/Serato-DJ-Suite-Free-Professional-DJ-Software` | lure_repo | not claimed |
| url | `https://github.com/ChromePheasant/Neural-DSP-Plugins-Free-Professional-Guitar-Bass-Production` | lure_repo | not claimed |
| url | `https://github.com/Wayvontitle2/Autodesk-Revit-2027-Free-Professional-BIM-Software` | lure_repo | not claimed |
| url | `https://github.com/magentacrabsoul/Native-Instruments-Traktor-Pro-4-Free-Professional-DJ-Software` | lure_repo | not claimed |
| url | `https://github.com/RestrictionCarpenter/iZotope-RX-12-Advanced-Free-Professional-Audio-Restoration` | lure_repo | not claimed |
| url | `https://github.com/ratequeenask/Native-Instruments-Guitar-Rig-7-Pro-Free-Guitar-Amp-Effects` | lure_repo | not claimed |
| url | `https://github.com/Gloryfromcall/Steinberg-SpectraLayers-Pro-13-Free-AI-Audio-Editing` | lure_repo | not claimed |
| url | `https://github.com/gpujouninravine/rekordbox-Professional-7-Free-Professional-DJ-Software` | lure_repo | not claimed |
| url | `https://github.com/MinotaurByteBond10/Twinmotion-2026-Free-Professional-Architectural-Visualization` | lure_repo | not claimed |
| url | `https://github.com/SkyGeomancer/Chaos-V-Ray-Collection-Free-Professional-3D-Rendering` | lure_repo | not claimed |
| url | `https://github.com/Galaxyeitriumph/Graphisoft-Archicad-29-Collaborate-Free-Professional-BIM-Design` | lure_repo | not claimed |
| url | `https://github.com/spirebossrescue/D5-Render-Teams-3.1.1-Free-Professional-3D-Rendering` | lure_repo | not claimed |
| url | `https://github.com/SheetMythStretch/Vectorworks-Architect-2027-Free-Professional-BIM-Design` | lure_repo | not claimed |
| url | `https://github.com/existenceblazecanyon/SOLIDWORKS-Design-Ultimate-2026-Free-Professional-3D-CAD` | lure_repo | not claimed |
| url | `https://github.com/LavaDeerHook/Autodesk-Inventor-Professional-2027-Free-3D-CAD-Design` | lure_repo | not claimed |
| url | `https://github.com/AnalystSucceed/HWID-Testing-Utility-Free-Hardware-ID-Management` | lure_repo | not claimed |
| url | `https://github.com/CoalSmokeMake/voicemod` | lure_repo | not claimed |
| url | `https://github.com/PulverizeFrogFigure/voicemod` | lure_repo | not claimed |
| url | `https://github.com/FloodChemistQuilt/voicemod` | lure_repo | not claimed |
| url | `https://github.com/cliffmotormanvolt38/winutilits` | lure_repo | not claimed |
| url | `https://github.com/PeakEconomicFetter/Filmora16-Ai-Editor-Plus` | lure_repo | not claimed |
| url | `https://github.com/limetempodemodulator/Microsoft-Power-BI-Pro` | lure_repo | not claimed |
| url | `https://github.com/ColorsSwanFlare/After-Effects` | lure_repo | not claimed |
| url | `https://github.com/AreaCounselorFurnace/EaseUS-Todo-Backup` | lure_repo | not claimed |
| url | `https://github.com/ForestBladesmith/Adobe-Audition-PC` | lure_repo | not claimed |
| url | `https://github.com/Modernlavilla/GTA6-PC` | lure_repo | not claimed |
| url | `https://github.com/SolarMistSay/REAPER-7.84-Free-Professional-Audio-Production` | lure_repo | not claimed |
| url | `https://github.com/beatlarkknow/Foundry-Nuke-Studio-Free-Download-VFX-Software` | lure_repo | not claimed |
| url | `https://github.com/Entityoverregister/FL-Studio-Free-Download-Modified-Edition` | lure_repo | not claimed |
| url | `https://github.com/creekspiderwrench/Neat-Video-Professional-Video-Noise-Reduction` | lure_repo | not claimed |
| url | `https://github.com/marblecashierdeflate/Adobe-After-Effects-Modified-Edition` | lure_repo | not claimed |
| url | `https://github.com/SoundCourier/Steinberg-Cubase-Music-Production-Software` | lure_repo | not claimed |
| url | `https://github.com/Sandglodepot35/Boris-FX-Suite-VFX-Motion-Graphics` | lure_repo | not claimed |
| url | `https://github.com/RetroDukeGrasp/CapCut-Pro-Advanced-Video-Editing-Software` | lure_repo | not claimed |
| url | `https://github.com/Goliathvubarrier/VEGAS-Pro-Professional-Video-Editing-Software` | lure_repo | not claimed |
| url | `https://github.com/AttorneyPrime/DVDFab-Enlarger-AI-Free-AI-Video-Upscaling` | lure_repo | not claimed |
| url | `https://github.com/Celestialdenlure/DaVinci-Resolve-Studio-Video-Editing-Color-Grading` | lure_repo | not claimed |
| url | `https://github.com/beingtyrantdescribe/Wondershare-Filmora-Premium-Video-Editing-Software` | lure_repo | not claimed |
| url | `https://github.com/LovebirdQuest/Mocha-Pro-Free-Download-Motion-Tracking-VFX` | lure_repo | not claimed |
| url | `https://github.com/SpikeEmissary/Avid-Pro-Tools-Ultimate-Free-Professional-Audio-Production` | lure_repo | not claimed |
| url | `https://github.com/HighwayPixel/Avid-Media-Composer-Professional-Video-Editing` | lure_repo | not claimed |
| url | `https://github.com/SageSpanner84/Cavalry-Free-2D-Animation-Motion-Graphics-Software` | lure_repo | not claimed |
| url | `https://github.com/GlazeFighter9/Maschine-3-Bundle-Free-Beat-Making-Music-Production` | lure_repo | not claimed |
| url | `https://github.com/opencolonelswell/Bitwig-Studio-6-Free-Professional-Music-Production` | lure_repo | not claimed |
| url | `https://github.com/Capturebrifence/Adobe-Audition-26.5-Professional-Audio-Editing` | lure_repo | not claimed |
| url | `https://github.com/ChauffeurMoon91/FilmLight-Baselight-v7-Free-Professional-Color-Grading` | lure_repo | not claimed |
| url | `https://github.com/PanelLocksmithSquare/Blackmagic-Fusion-Studio-21-Free-Professional-VFX` | lure_repo | not claimed |
| url | `https://github.com/handcuffrajarepair/Adobe-Premiere-Pro-Free-Professional-Video-Editing` | lure_repo | not claimed |
| url | `https://github.com/macrosergeantsquare/Native-Instruments-Massive-X-1.7-Free-Professional-Synthesizer` | lure_repo | not claimed |
| url | `https://github.com/RealRegionKind/iZotope-Ozone-12-Advanced-Free-Professional-Audio-Mastering` | lure_repo | not claimed |
| url | `https://github.com/Psycheoftrim36/Spitfire-Audio-BBC-Symphony-Orchestra-Professional-Free` | lure_repo | not claimed |
| url | `https://github.com/Torrentdreinferno/EastWest-ComposerCloud-Free-Premium-Virtual-Instruments` | lure_repo | not claimed |
| url | `https://github.com/Slowgrerhythm/Xfer-Serum-2-Free-Professional-Wavetable-Synthesizer` | lure_repo | not claimed |
| url | `https://github.com/LusterJouninAtone25/Spectrasonics-Omnisphere-3-Free-Professional-Synthesizer` | lure_repo | not claimed |
| url | `https://github.com/BreezeFlamingoGorge/Sound-Forge-Plus-2026-Free-Professional-Audio-Editing` | lure_repo | not claimed |
| url | `https://github.com/ComponentSupplier/Waves-Ultimate-V17-Free-Professional-Audio-Plugins` | lure_repo | not claimed |
| url | `https://github.com/dreamcyclevoyage/Plugin-Alliance-PRO-Free-Professional-Audio-Plugins` | lure_repo | not claimed |
| url | `https://github.com/RouteShelter/Arturia-Pigments-7-Free-Professional-Synthesizer` | lure_repo | not claimed |
| url | `https://github.com/Shellfespiral/Native-Instruments-Kontakt-8-Full-Free-Professional-Sampler` | lure_repo | not claimed |
| url | `https://github.com/PointAirRecover56/Wise-Care` | lure_repo | not claimed |
| url | `https://github.com/Rhythmtrualter/Wise-Registrity` | lure_repo | not claimed |
| url | `https://github.com/silverindustrialgap/Auslogics` | lure_repo | not claimed |
| url | `https://github.com/RopemakerCoil/Burning-Studio` | lure_repo | not claimed |
| url | `https://github.com/sandsheriffbeat/Cinebench` | lure_repo | not claimed |
| url | `https://github.com/SegmentWarden/Data-Grip` | lure_repo | not claimed |
| url | `https://github.com/squareswimmeryell/Easy-Worship` | lure_repo | not claimed |
| url | `https://github.com/SplendorCooper/ExitLag` | lure_repo | not claimed |
| url | `https://github.com/StylistMultiplexer/HitFilm` | lure_repo | not claimed |
| url | `https://github.com/symboladvocateshaft/KeyShot-Pro` | lure_repo | not claimed |
| url | `https://github.com/VaultAssurance/PHP-Storm` | lure_repo | not claimed |
| url | `https://github.com/wellflashalter/RX-11-Audio-Editor` | lure_repo | not claimed |
| url | `https://github.com/vortexlakecanal/Rufus` | lure_repo | not claimed |
| url | `https://github.com/Wyrmfosafeguard/Sylenth-1` | lure_repo | not claimed |
| url | `https://github.com/yarnvoicedesignate/ultra-Iso` | lure_repo | not claimed |
| url | `https://github.com/MediatorRevive/CCleaner-Pro` | lure_repo | not claimed |
| url | `https://github.com/Attodreslicer/drphone-data-recovery` | lure_repo | not claimed |
| url | `https://github.com/56411952/aion-2-enhancement-suite` | lure_repo | not claimed |
| url | `https://github.com/foursixity001-hub/aion-2-enhancement-suite` | lure_repo | not claimed |
| url | `https://github.com/joaopedro903/delta-executor-desktop-toolkit` | lure_repo | not claimed |
| url | `https://github.com/GpiceQ/inventor-desktop-installer` | lure_repo | not claimed |
| url | `https://github.com/Hubkrereanimate/Secure-PDF-Workstation` | lure_repo | not claimed |
| url | `https://github.com/Omegaofidolize/ableton-live-12` | lure_repo | not claimed |
| url | `https://github.com/phantomsociallook/auslogics` | lure_repo | not claimed |
| url | `https://github.com/Pointyodemolish/bloxshade-for-roblox` | lure_repo | not claimed |
| url | `https://github.com/PlanetCraneInterface/autodesk-revit` | lure_repo | not claimed |
| url | `https://github.com/platooncaptainmarket/better-discord` | lure_repo | not claimed |
| url | `https://github.com/QuakeAdmiral/crash-plan` | lure_repo | not claimed |
| url | `https://github.com/ShackleCosmetologist/genesis-scanner` | lure_repo | not claimed |
| url | `https://github.com/shalecorporatelabel/grayket` | lure_repo | not claimed |
| url | `https://github.com/SmokeObliterate/imyfone` | lure_repo | not claimed |
| url | `https://github.com/SphereMagistrate39/metatrader` | lure_repo | not claimed |
| url | `https://github.com/TerminusPotter/quant-trading-bot` | lure_repo | not claimed |
| url | `https://github.com/VillageExecutive/ultra-edit` | lure_repo | not claimed |
| url | `https://github.com/VolcanoBaseCock/voicechanger` | lure_repo | not claimed |
| url | `https://github.com/WeaponsmithPray/winutilits` | lure_repo | not claimed |
| url | `https://github.com/WeaveSeekerJinx/wise-care` | lure_repo | not claimed |
| url | `https://github.com/Falsetervitalize/discord-server-raider` | lure_repo | not claimed |
| url | `https://github.com/gripdiplomatendure1/melodyne-5` | lure_repo | not claimed |
| url | `https://github.com/gryphonduckdefend/microsoft-office` | lure_repo | not claimed |
| url | `https://github.com/Grottoflachain/microsoft-365` | lure_repo | not claimed |
| url | `https://github.com/hopegiraffestride/movavi-video-editor-plus` | lure_repo | not claimed |
| url | `https://github.com/JumperCrater/pump-fun` | lure_repo | not claimed |
| url | `https://github.com/MechanicClaim/total-commander` | lure_repo | not claimed |
| url | `https://github.com/mortalswanstrait/wise-care` | lure_repo | not claimed |
| url | `https://github.com/DeimosPhobos666/office-suite-validator` | lure_repo | not claimed |
| url | `https://github.com/rimoharp/melodyne-5` | lure_repo | not claimed |

## Files

| SHA-256 |
| --- |
| `fbaeb724f58c6c90c38e1af9333b265dabe6e6f78509b47a21da9f9db0db23ec` |
| `75cae8dc8680c83a30588f24bfb2902071396117b8fd48a982f8ab8d031ecc9d` |
| `df3a3973900153a363e21385ca3394addac8d52c7547827dc334ebff75ee451b` |
| `9f293cda819b74342bb598291010ee02a96af71eb2dabc7ab4c94edea21afa9c` |
