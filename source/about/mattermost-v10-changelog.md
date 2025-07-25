# v10 Changelog

```{Important}
```{include} common-esr-support-upgrade.md
```

(release-v10.10-feature-release)=
## Release v10.10 - [Feature Release](https://docs.mattermost.com/about/release-policy.html#release-types)

- **10.10.1, released 2025-07-16**
  - Mattermost v10.10.1 contains medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release as soon as possible is highly recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Mattermost v10.10.1 contains no database or functional changes.
- **10.10.0, released 2025-07-16**
  - Original 10.10.0 release.

### Important Upgrade Notes
 - Added a new column ``DefaultCategoryName`` to the ``Channels`` table. This is nullable and stores a category name to be added/created when new users join a channel. This is only used if the ``ExperimentalChannelCategorySetting`` is enabled. No database downtime is expected for this upgrade. See the [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html) for more details.
 - Added new columns ``RemoteId`` and ``ChannelId`` to the ``PostAcknowledgements`` table. No database downtime is expected for this upgrade. See the [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html) for more details.
 - Added a new column ``LastMembersSyncAt`` to the ``SharedChannelRemotes`` table and added ``LastMembershipSyncAt`` to ``SharedChannelUsers``. No database downtime is expected for this upgrade. See the [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html) for more details.
 - Added a new column ``LastGlobalUserSyncAt`` to the ``RemoteClusters`` table. No database downtime is expected for this upgrade. See the [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html) for more details.

```{Important}
If you upgrade from a release earlier than v10.9, please read the other [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html).
```

### Improvements

#### User Interface (UI)
 - Pre-packaged Calls plugin [v1.9.1](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.9.1).
 - Pre-packaged GitLab plugin [v1.10.0](https://github.com/mattermost/mattermost-plugin-gitlab/releases/tag/v1.10.0).
 - Pre-packaged GitHub plugin [v2.4.0](https://github.com/mattermost/mattermost-plugin-github/releases/tag/v2.4.0).
 - Pre-packaged Boards plugin [v9.1.4](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.1.4).
 - Pre-packaged Agents plugin [v1.2.4](https://github.com/mattermost/mattermost-plugin-agents/releases/tag/v1.2.4).
 - Resolved inconsistent styling issues in new integration pages.
 - Improved the visual styling of blockquotes and comment threads for better readability and a modern appearance.
 - Improved screen reader support for autocompletes and channel switcher.
 - Added an aria-live region for improved accessibility of file preview modal carousel position updates.
 - Add focusability to react-select remove button in notifications settings.
 - Updated **Profile** settings client-side validation to use more modern/accessible paradigms.
 - Enhanced the accessibility of login and password reset functionality.
 - Stopped the Threads textbox from automatically taking focus when it contained a draft.
 - Added a display setting for users to toggle rendering of emoticons (e.g., :D) as emojis (e.g., 😄).
 - Added support for the ``from:`` search filter in cross-team searches.
 - Standardized button styling by consolidating color variables and removing redundant theme definitions.
 - Ignored email domain in user searches on the client side.
 - Automatically detected and updated timezone changes without requiring a client refresh.

#### Administration
 - Added support for group messages in Shared Channels.
 - Added new feature flags (default off) ``EnableSharedChannelsMemberSync`` and ``EnableSyncAllUsersForRemoteCluster`` for Connected Workspaces.
 - Hid plugin components in Shared Channels and introduced ``EnableSharedChannelsPlugins`` to re-enable them if needed.
 - Added an LDAP Wizard with various enhancements, including a **Test Group Attributes** button for feedback on matching group attributes, a **Test Connection** button with improved error reporting, a **Test Attributes** button showing attribute success and matching user count, a **Test Filters** button with failure feedback, an expandable **User Filters** section with "More info" hover texts, and a help text explaining the possible delay when running tests on large LDAP servers.
 - Added support for licenses that enforce seat counts with a configurable ``ExtraUsers`` field for exact control over allowed overages.
 - Organized cluster files into directories for the Support Packet.
 - Partially sanitized database datasources for the Support Packet.
 - Added deactivation status to the mmctl user search output.

#### Performance
 - Improved memory performance of post list scrolling.
 - Improved the performance of sidebar update APIs slightly.

### Bug Fixes
 - Fixed an issue where a ``MESSAGES`` badge appeared in the search bar after clearing text and closing the search box.
 - Fixed an issue where overridden webhook usernames did not appear in replies when Threaded Discussions were disabled.
 - Fixed indentation issues in Markdown lists containing checkboxes.
 - Fixed desktop notifications for posts without text content to display "posted a message" instead of "did something new".
 - Fixed the height of the automatic replies text area to align with proper dimensions.
 - Fixed various accessibility issues in the User Groups modals.
 - Fixed accessibility issues in Profile Settings to enhance usability.
 - Fixed dialog dropdowns to ensure they were not cut off visually.
 - Fixed an issue where deactivated users still maintained their previous status.
 - Fixed an issue with plugin dialogs triggering errors upon submission.
 - Fixed the version number of Support Packet v2.
 - Fixed an issue with MIME type detection for video files (e.g., MP4, MOV, AVI, WEBM, WMV, MKV, MPG/MPEG) uploaded to S3 storage, enabling inline video playback in browsers.
 - Fixed Support Packet caching issues.
 - Fixed the **Threads** textbox changing width when a message was typed on certain screens.
 - Fixed an issue with log messages including blank "user_id" field when request session was not valid or had a blank user_id.
 - Fixed an issue where the emoji picker focus did not return to button when not selecting an emoji.
 - Fixed the label in notification settings for the notification sound combo box.
 - Fixed an issue where an incorrect username and email were shown for remote users.
 - Fixed an issue with the keyboard navigation in the user settings sidebar.

### config.json
New setting options were added to ``config.json``. Below is a list of the additions and their default values on install. The settings can be modified in ``config.json``, or the System Console when available.

#### Changes to all plans:
 - Under ``ExperimentalSettings`` in ``config.json``:
    - Added ``ExperimentalChannelCategorySorting`` configuration setting to add the ability to automatically sort channels into categories upon creation/renaming.

#### Changes to Enterprise plan:
 - Under ``DataRetentionSettings`` in ``config.json``:
    - Added ``PreservePinnedPosts`` configuration setting. If it's set to ``true``, pinned posts will not be deleted by data retention. 

#### Changes to Enterprise Advanced plan:
 - Under ``ConnectedWorkspacesSettings`` in ``config.json``:
    - Added ``MemberSyncBatchSize``, ``SyncUsersOnConnectionOpen``, ``GlobalUserSyncBatchSize`` configuration settings to allow remote users to be discoverable in the Direct/Group Message modal. 

### API Changes
 - Added property fields and value methods to the plugin API.
 - Improved the semantics of Groups API errors when invalid parameters were specified.

### Open Source Components
 - Added ``mholt/archives`` and removed ``code.sajari.com/docconv`` from https://github.com/mattermost/mattermost.

### Go Version
 - v10.10 is built with Go ``v1.24.3``.

### Contributors
 - [abbas-dependable-naqvi](https://github.com/abbas-dependable-naqvi), [agarciamontoro](https://github.com/agarciamontoro), [agnivade](https://github.com/agnivade), [Akhilbisht798](https://github.com/Akhilbisht798), [amyblais](https://github.com/amyblais), [andrleite](https://github.com/andrleite), [angeloskyratzakos](https://github.com/angeloskyratzakos), [Aryakoste](https://github.com/Aryakoste), [AulakhHarsh](https://github.com/AulakhHarsh), [BenCookie95](https://github.com/BenCookie95), [calebroseland](https://github.com/calebroseland), [Carloswaldo](https://translate.mattermost.com/user/Carloswaldo), [catalintomai](https://github.com/catalintomai), [coltoneshaw](https://github.com/coltoneshaw), [cpoile](https://github.com/cpoile), [crspeller](https://github.com/crspeller), [ctlaltdieliet](https://translate.mattermost.com/user/ctlaltdieliet), [cwarnermm](https://github.com/cwarnermm), [davidkrauser](https://github.com/davidkrauser), [devinbinnie](https://github.com/devinbinnie), [Ekaterine](https://translate.mattermost.com/user/Ekaterine), [EkaterinePapava](https://github.com/EkaterinePapava), [enahum](https://github.com/enahum), [enzowritescode](https://github.com/enzowritescode), [equalsgibson](https://github.com/equalsgibson), [esarafianou](https://github.com/esarafianou), [ewwollesen](https://github.com/ewwollesen), [fmartingr](https://github.com/fmartingr), [frankps](https://translate.mattermost.com/user/frankps), [fsilye](https://github.com/fsilye), [gabrieljackson](https://github.com/gabrieljackson), [hannaparks](https://github.com/hannaparks), [hanzei](https://github.com/hanzei), [harshilsharma63](https://github.com/harshilsharma63), [hmhealey](https://github.com/hmhealey), [iamleson98](https://github.com/iamleson98), [irdi-cloud68](https://translate.mattermost.com/user/irdi-cloud68), [isacikgoz](https://github.com/isacikgoz), [johnsonbrothers](https://github.com/johnsonbrothers), [jprusch](https://github.com/jprusch), [JulienTant](https://github.com/JulienTant), [jwilander](https://github.com/jwilander), [kaakaa](https://github.com/kaakaa), [kasyap1234](https://github.com/kasyap1234), [Kshitij-Katiyar](https://github.com/Kshitij-Katiyar), [larkox](https://github.com/larkox), [ldez](https://github.com/ldez), [lieut-data](https://github.com/lieut-data), [lindalumitchell](https://github.com/lindalumitchell), [M-ZubairAhmed](https://github.com/M-ZubairAhmed), [majo](https://translate.mattermost.com/user/majo), [mansil](https://github.com/mansil), [marianunez](https://github.com/marianunez), [master7](https://translate.mattermost.com/user/master7), [matt-w99](https://github.com/matt-w99), [matthew-w](https://translate.mattermost.com/user/matthew-w), [matthewbirtch](https://github.com/matthewbirtch), [mgdelacroix](https://github.com/mgdelacroix), [Morgansvk](https://github.com/Morgansvk), [neil-karania](https://github.com/neil-karania), [nickmisasi](https://github.com/nickmisasi), [panoramix360](https://github.com/panoramix360), [polinapianina](https://github.com/polinapianina), [pvev](https://github.com/pvev), [rahimrahman](https://github.com/rahimrahman), [Rajat-Dabade](https://github.com/Rajat-Dabade), [Reinkard](https://github.com/Reinkard), [saturninoabril](https://github.com/saturninoabril), [sbishel](https://github.com/sbishel), [Sharuru](https://github.com/Sharuru), [spirosoik](https://github.com/spirosoik), [stafot](https://github.com/stafot), [streamer45](https://github.com/streamer45), [svelle](https://github.com/svelle), [uday-rana](https://github.com/uday-rana), [Victor-Nyagudi](https://github.com/Victor-Nyagudi), [wiersgallak](https://github.com/wiersgallak), [wiggin77](https://github.com/wiggin77), [Willyfrog](https://github.com/Willyfrog), [yasserfaraazkhan](https://github.com/yasserfaraazkhan)

(release-v10.9-feature-release)=
## Release v10.9 - [Feature Release](https://docs.mattermost.com/about/release-policy.html#release-types)

- **10.9.4, released 2025-07-22**
  - Mattermost v10.9.4 contains medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release as soon as possible is highly recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Mattermost v10.9.4 contains no database or functional changes.
- **10.9.3, released 2025-07-08**
  - Mattermost v10.9.3 contains medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release as soon as possible is highly recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Boards plugin version [v9.1.4](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.1.4).
  - Fixed an issue with the keyboard navigation in the user settings sidebar [MM-64669](https://mattermost.atlassian.net/browse/MM-64669).
  - Mattermost v10.9.3 contains no database or functional changes.
- **10.9.2, released 2025-06-19**
  - Mattermost v10.9.2 contains a medium severity level security fix. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release as soon as possible is highly recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Mattermost v10.9.2 contains no database or functional changes.
- **10.9.1, released 2025-06-17**
  - Mattermost v10.9.1 contains a medium severity level security fix. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release as soon as possible is highly recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Fixed an issue where Direct/Group Messages were missing on initial load [MM-64481](https://mattermost.atlassian.net/browse/MM-64481).
  - Pre-packaged Boards plugin version [v9.1.3](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.1.3).
  - Mattermost v10.9.1 contains no database or functional changes.
- **10.9.0, released 2025-06-16**
  - Original 10.9.0 release.

### Compatibility
 - Updated the minimum supported versions of Edge and Chrome to 134+, and Firefox to 128+.

### Important Upgrade Notes
 - A new index to the ``CategoryId`` column in ``SidebarChannels`` table was added to improve query performance. No database downtime is expected for this upgrade. See the [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html) for more details.
 - Schema changes in the form of a new materialized view (``AttributeView``) was added that aggregates user attributes into a separate table. No database downtime is expected for this upgrade. See the [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html) for more details.

```{Important}
If you upgrade from a release earlier than v10.8, please read the other [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html).
```

### Highlights

#### New Enterprise Advanced License
 - Added support for a new Enterprise Advanced license. This new license is supported starting v10.9 and is supported on PostgreSQL only. Enterprise plugins need to be updated to support the new license (most of which are pre-packaged in v10.9).

### Improvements

#### User Interface (UI)
 - Consolidated all channel editing functionality into a single, accessible modal located in the channel header menu. Users can now update channel names, URL slugs, convert to private, modify/add a purpose and header (with a live markdown preview), manage channel banners, and archive the channel—all in one place. Updates include safeguards for unsaved edits, improved URL-slug editing, and enhanced keyboard and navigation accessibility.
 - Pre-packaged MS Teams plugin [v2.2.1](https://github.com/mattermost/mattermost-plugin-msteams/releases/tag/v2.2.1).
 - Pre-packaged Playbooks plugin [v2.2.0](https://github.com/mattermost/mattermost-plugin-playbooks/releases/tag/v2.2.0) and [v1.41.1](https://github.com/mattermost/mattermost-plugin-playbooks/releases/tag/v1.41.1).
 - Pre-packaged Calls plugin [v1.8.0](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.8.0).
 - Pre-packaged Jira plugin version [v4.3.0](https://github.com/mattermost/mattermost-plugin-jira/releases/tag/v4.3.0).
 - Pre-packaged Metrics plugin version [v0.7.0](https://github.com/mattermost/mattermost-plugin-metrics/releases/tag/v0.7.0).
 - Introduced a configurable channel banner feature for channel admins, visible across desktop, web, and mobile platforms. This feature requires an Enterprise Advanced license.
 - Added more descriptive page titles to the login, account creation, and password reset pages.
 - Improved the **Drafts** list by implementing virtualization.
 - Enhanced the behavior for reporting issues in the platform.
 - Introduced minor layout tweaks in theme settings for improved usability.

#### Administration
 - Added support for user attributes for Enterprise Advanced licensed servers. Defined policies that automatically grant channel memberships based on user attributes. Membership updates happen automatically when user attributes change — no need for manual role adjustments.
 - Added Policy Management user interface and API to easily create and manage attribute-based rules via an admin interface.
 - Added support for AES-256-GCM encryption in SAML.
 - Updated the email validation logic to ensure Mattermost no longer accepts email addresses enclosed in angle brackets (e.g., ``<billy@example.com>``). Although these comply with RFC 5322 and RFC 6532 standards, they introduce unnecessary complexity. If a user already has such an email in your installation, they may face issues like being unable to update their profile. To resolve this, the email must be modified manually using the command: ``mmctl user email "<affecteduser@domain.com>" affecteduser@domain.com``.
 - Added a license load metric to the **About** screen to display current license usage.
 - Upgraded the logr dependency to version 2.0.22.
 - Removed telemetry tracking from Redux selectors.
 - Made it possible to view JSON logs in plain text within the **System Console**.
 - Enhanced the **System Console** search functionality to include all log fields.
 - Enhanced error reporting related to cluster management.
 - Added an LDAP setting to re-add removed members.
 - Added support for SSO while Mattermost is embedded in an iframe.
 - Set the Custom Profile Attributes feature flag to ``true`` by default.

#### Performance
 - Optimized the team-switching operation by eliminating unnecessary calls to retrieve channels and channel members.
 - Improved websocket re-opening speed when network conditions change.

### Bug Fixes
 - Fixed various issues on the **Create Team** screen.
 - Fixed several accessibility issues across the login process, account creation, and MFA setup.
 - Fixed an issue where horizontal rule (HR) elements were not visible in preview mode in the right-hand sidebar (RHS).
 - Fixed an issue with inconsistent sizing of markdown images in preview mode.
 - Fixed a keyboard navigation issue within thread items.
 - Fixed layout issues with the emoji picker on mobile browsers.
 - Fixed an issue with the positioning of **Edited** text and tooltips in certain scenarios.
 - Fixed the accessibility of the search box.
 - Fixed an issue where post list scrolling didn’t work when pressing the **Page Up** or **Page Down** keys.
 - Fixed issues with screen reader support in the **Threads** view.
 - Fixed keyboard navigation issues in the **Threads** view.
 - Fixed accessibility issues in the **Invite** modal.
 - Fixed various accessibility issues in the **Browse Channels** modal.
 - Fixed an issue that prevented team admin permissions from being modified when missing in the **All Members** section.
 - Fixed possible deadlocks when updating ``SidebarCategories`` and ``SidebarChannels`` tables.
 - Fixed an issue where unreads from deleted teams would display in the titlebar/Desktop App.
 - Fixed an issue with ``icon_emoji`` property not working for webhook posts.

### config.json
New setting options were added to ``config.json``. Below is a list of the additions and their default values on install. The settings can be modified in ``config.json``, or the System Console when available.

#### Changes to all plans:
 - Under ``SupportSettings`` in ``config.json``:
    - Added ``ReportAProblemType``, ``ReportAProblemMail``, ``AllowDownloadLogs`` configuration settings to enhance the behavior for reporting issues in the platform.

#### Changes to Enterprise plans:
 - Under ``ExperimentalAuditSettings`` in ``config.json``:
    - Added ``Certificate`` configuration setting to accept a certificate to be used for audit logging egress.
 - Under ``LdapSettings`` in ``config.json``:
    - Added ``ReAddRemovedMembers`` configuration setting to add a LDAP setting to re-add removed members.

### API Changes
 - Exposed two new plugin APIs for syncables.

### Open Source Components
 - Added ``monaco-editor`` and ``monaco-editor-webpack-plugin``, and removed ``dynamic-virtualized-list``, ``popper.js``, ``react-hot-loader``, ``react-popper`` from https://github.com/mattermost/mattermost.

### Go Version
 - v10.9 is built with Go ``v1.23.7``.

### Known Issues
 - Permissions lists exceed content area for **All Members** and **System Admins** in the System Console [MM-64417](https://mattermost.atlassian.net/browse/MM-64417).
 - Setting the license file location through an environment variable still gives the option to upload a new license through the System Console, resulting in the license being overwritten by the one set through the environment variable. See this [knowledge base article](https://support.mattermost.com/hc/en-us/articles/33911983851284-System-console-still-displays-old-license-after-uploading-a-new-one) on how to resolve this issue.

### Contributors
 - [agarciamontoro](https://github.com/agarciamontoro), [agnivade](https://github.com/agnivade), [amyblais](https://github.com/amyblais), [andrleite](https://github.com/andrleite), [angeloskyratzakos](https://github.com/angeloskyratzakos), [AnmiTaliDev](https://translate.mattermost.com/user/AnmiTaliDev), [Aryakoste](https://github.com/Aryakoste), [AshishDhama](https://github.com/AshishDhama), [AulakhHarsh](https://github.com/AulakhHarsh), [BenCookie95](https://github.com/BenCookie95), [bndn](https://translate.mattermost.com/user/bndn), [bshumylo](https://github.com/bshumylo), [calebroseland](https://github.com/calebroseland), [catalintomai](https://github.com/catalintomai), [chicchu4157](https://translate.mattermost.com/user/chicchu4157), [cinlloc](https://github.com/cinlloc), [coltoneshaw](https://github.com/coltoneshaw), [cpoile](https://github.com/cpoile), [crspeller](https://github.com/crspeller), [ctlaltdieliet](https://translate.mattermost.com/user/ctlaltdieliet), [cwarnermm](https://github.com/cwarnermm), [cyrusjc](https://github.com/cyrusjc), [danilvalov](https://github.com/danilvalov), [davidkrauser](https://github.com/davidkrauser), [devinbinnie](https://github.com/devinbinnie), [enahum](https://github.com/enahum), [esarafianou](https://github.com/esarafianou), [evituzas](https://translate.mattermost.com/user/evituzas), [fmartingr](https://github.com/fmartingr), [frankps](https://translate.mattermost.com/user/frankps), [fsilye](https://github.com/fsilye), [gabrieljackson](https://github.com/gabrieljackson), [gentcod](https://github.com/gentcod), [Gesare5](https://github.com/Gesare5), [guenjun](https://translate.mattermost.com/user/guenjun), [hannaparks](https://github.com/hannaparks), [hanzei](https://github.com/hanzei), [harshilsharma63](https://github.com/harshilsharma63), [hmhealey](https://github.com/hmhealey), [isacikgoz](https://github.com/isacikgoz), [iyampaul](https://github.com/iyampaul), [jespino](https://github.com/jespino), [johnsonbrothers](https://github.com/johnsonbrothers), [joho1968](https://github.com/joho1968), [jprusch](https://github.com/jprusch), [JulienTant](https://github.com/JulienTant), [jwilander](https://github.com/jwilander), [kaakaa](https://github.com/kaakaa), [kasyap1234](https://github.com/kasyap1234), [kayazeren](https://translate.mattermost.com/user/kayazeren), [Kimbohlovette](https://github.com/Kimbohlovette), [Kshitij-Katiyar](https://github.com/Kshitij-Katiyar), [larkox](https://github.com/larkox), [ldez](https://github.com/ldez), [lieut-data](https://github.com/lieut-data), [lindy65](https://github.com/lindy65), [lynn915](https://github.com/lynn915), [M-ZubairAhmed](https://github.com/M-ZubairAhmed), [majo](https://translate.mattermost.com/user/majo), [mansil](https://github.com/mansil), [marcelhintermann](https://github.com/marcelhintermann), [marianunez](https://github.com/marianunez), [master7](https://translate.mattermost.com/user/master7), [matthewbirtch](https://github.com/matthewbirtch), [mgdelacroix](https://github.com/mgdelacroix), [Morgansvk](https://github.com/Morgansvk), [nickmisasi](https://github.com/nickmisasi), [oonid](https://translate.mattermost.com/user/oonid), [panoramix360](https://github.com/panoramix360), [pineoak-audio](https://github.com/pineoak-audio), [pvev](https://github.com/pvev), [raghavaggarwal2308](https://github.com/raghavaggarwal2308), [rahimrahman](https://github.com/rahimrahman), [Rajat-Dabade](https://github.com/Rajat-Dabade), [Reinkard](https://github.com/Reinkard), [rOt779kVceSgL](https://translate.mattermost.com/user/rOt779kVceSgL), [sadohert](https://github.com/sadohert), [saturninoabril](https://github.com/saturninoabril), [sbishel](https://github.com/sbishel), [Sharuru](https://translate.mattermost.com/user/Sharuru), [stafot](https://github.com/stafot), [streamer45](https://github.com/streamer45), [svelle](https://github.com/svelle), [Theo024](https://github.com/Theo024), [ThrRip](https://github.com/ThrRip), [toninis](https://github.com/toninis), [Vasfed](https://github.com/Vasfed), [vasilybels](https://github.com/vasilybels), [VDALuky](https://github.com/VDALuky), [vish9812](https://github.com/vish9812), [wiersgallak](https://github.com/wiersgallak), [wiggin77](https://github.com/wiggin77), [Willyfrog](https://github.com/Willyfrog), [yasserfaraazkhan](https://github.com/yasserfaraazkhan)

(release-v10.8-feature-release)=
## Release v10.8 - [Feature Release](https://docs.mattermost.com/about/release-policy.html#release-types)

- **10.8.4, released 2025-07-22**
  - Mattermost v10.8.4 contains medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release as soon as possible is highly recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Boards plugin version [v9.1.4](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.1.4).
  - Mattermost v10.8.4 contains no database or functional changes.
- **10.8.3, released 2025-06-18**
  - Mattermost v10.8.3 contains a medium severity level security fix. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Playbooks plugin [v1.41.1](https://github.com/mattermost/mattermost-plugin-playbooks/releases/tag/v1.41.1).
  - Pre-packaged Boards plugin version [v9.1.3](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.1.3).
  - Fixed an issue where the ``icon_emoji`` property was not working for webhook posts [MM-64316](https://mattermost.atlassian.net/browse/MM-64316).
  - Added support for SSO while Mattermost is embedded in an iframe [MM-63900](https://mattermost.atlassian.net/browse/MM-63900).
  - Mattermost v10.8.3 contains no database or functional changes.
- **10.8.2, released 2025-05-29**
  - Mattermost v10.8.2 contains high severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged MS Teams plugin [v2.2.1](https://github.com/mattermost/mattermost-plugin-msteams/releases/tag/v2.2.1).
  - Mattermost v10.8.2 contains no database or functional changes.
- **10.8.1, released 2025-05-21**
  - Mattermost v10.8.1 contains a Critical severity level security fix. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release as soon as possible is highly recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Playbooks plugin [v2.2.0](https://github.com/mattermost/mattermost-plugin-playbooks/releases/tag/v2.2.0).
  - Fixed an issue where Team Admin permissions couldn't be changed if they were missing in **All members** section [MM-64157](https://mattermost.atlassian.net/browse/MM-64157).
  - Updated ``golang.org/x/net`` version to v0.39.0.
  - Mattermost v10.8.1 contains no database or functional changes.
- **10.8.0, released 2025-05-16**
  - Original 10.8.0 release.

### Important Upgrade Notes
 - New tables ``AccessControlPolicies`` and ``AccessControlPolicyHistory`` will be created. The migration is fully backwards-compatible, non-locking, and zero downtime is expected.
 - Support for legacy SKUs E10 and E20 licenses was removed. If you need assistance, [talk to a Mattermost expert](https://mattermost.com/contact-sales/).

```{Important}
If you upgrade from a release earlier than v10.7, please read the other [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html).
```

### Improvements

#### User Interface (UI)
 - Pre-packaged Calls plugin version [v1.7.1](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.7.1).
 - Pre-packaged Metrics plugin version [v0.6.0](https://github.com/mattermost/mattermost-plugin-metrics/releases/tag/v0.6.0).
 - Added an improved channel menu. 
 - Updated email notification settings to provide clearer wording and descriptions for both batched and non-batched scenarios. The settings dialog now reflects the selected status more accurately in both collapsed and expanded views, enhancing consistency and usability.
 - Added the ability to display the nickname or full name in Threads based on settings.
 - Improved the error message for failed file copies. 

#### Administration
 - Added Custom Profile Attribute field type, visibility, and related options in **System Console -> System Properties**.
 - Added support for LDAP/SAML sync with Custom Profile Attributes (disabled behind a feature flag).
 - Stopped building and packaging Windows and MacOS releases. 
 - ``EnableLocalMode`` is now automatically enabled during development. 
 - Log messages are now added if post props are invalid. 
 - Stopped logging websocket PING events received by the server. 
 - Errors from Support Packet generation are now shown in the **System Console**. 
 - Added a client-side ping to the websocket to detect broken connections more quickly.
 - Removed the feature flag and added a ``EnableCrossTeamSearch`` configuration option for cross-team search feature. 

### Bug Fixes
 - Fixed ``GET /groups endpoint`` documentation. 
 - Fixed an issue with group mentions overlay and details after an update. 
 - Fixed an issue with showing local hours on bot users. 
 - Fixed an issue where replies appeared as part of the wrong thread when Collapsed Reply Threads were disabled. 
 - Fixed an issue with keyboard input not working on new menus when the menu was opened using the mouse. 
 - Fixed an issue with keyboard navigation with the channel switcher. 
 - Fixed an issue with link previews when using angle brackets for autolinking. 
 - Fixed an issue where **Recent Mentions** showed incorrect results for custom notification keywords containing hyphens. 
 - Fixed an issue where there were invalid restrictions on local mode administration (e.g. via mmctl). 
 - Fixed an issue where users were not able to escape emoticon formatting by prefixing with a backslash. 
 - Fixed an issue with post links trapping focus when hovered or focused using the keyboard.
 - Fixed an issue where plugins were disabled when Mattermost was embedded.

### config.json
New setting options were added to ``config.json``. Below is a list of the additions and their default values on install. The settings can be modified in ``config.json``, or the System Console when available.

#### Changes to Enterprise plans:
 - Under ``AccessControlSettings`` in ``config.json``:
   - Added ``EnableAttributeBasedAccessControl`` and ``EnableChannelScopeAccessControl`` configuration settings. 
 - Under ``ServiceSettings`` in ``config.json``:
   - Added a ``EnableCrossTeamSearch`` configuration option for cross-team search feature.
 - Under ``ElasticsearchSettings`` in ``config.json``:
   - Added a new configuration setting ``GlobalSearchPrefix`` which can be used to search across multiple indices having a common prefix. This is useful in a scenario with multiple Elasticsearch instances, where multiple instances are writing to different indices with different prefixes using the ``ElasticsearchSettings.IndexPrefix`` setting. 

### API Changes
 - Added a new API endpoint to retrieve the Custom Profile Attributes group data. 

### Open Source Components
 - Added ``bep/imagemeta`` and removed ``rwcarlsen/goexif`` from https://github.com/mattermost/mattermost.

### Go Version
 - v10.8 is built with Go ``v1.23.7``.

### Known Issues
 - The ``icon_emoji`` property does not work for webhook posts [MM-64316](https://mattermost.atlassian.net/browse/MM-64316).
 - Setting the license file location through an environment variable still gives the option to upload a new license through the System Console, resulting in the license being overwritten by the one set through the environment variable. See this [knowledge base article](https://support.mattermost.com/hc/en-us/articles/33911983851284-System-console-still-displays-old-license-after-uploading-a-new-one) on how to resolve this issue.
 - Searching stop words in quotation marks with Elasticsearch enabled returns more than just the searched terms.
 - Slack import through the CLI fails if email notifications are enabled.

### Contributors
 - [aboukhal](https://github.com/aboukhal), [acc0mplish-note](https://translate.mattermost.com/user/acc0mplish-note), [agarciamontoro](https://github.com/agarciamontoro), [agnivade](https://github.com/agnivade), [amyblais](https://github.com/amyblais), [andrleite](https://github.com/andrleite), [angeloskyratzakos](https://github.com/angeloskyratzakos), [Arusekk](https://translate.mattermost.com/user/Arusekk), [Aryakoste](https://github.com/Aryakoste), [AshiishKarhade](https://github.com/AshiishKarhade), [AulakhHarsh](https://github.com/AulakhHarsh), [BenCookie95](https://github.com/BenCookie95), [bndn](https://github.com/bndn), [bshumylo](https://github.com/bshumylo), [burakcakirel](https://github.com/burakcakirel), [calebroseland](https://github.com/calebroseland), [catalintomai](https://github.com/catalintomai), [cpoile](https://github.com/cpoile), [crspeller](https://github.com/crspeller), [ctlaltdieliet](https://github.com/ctlaltdieliet), [cwarnermm](https://github.com/cwarnermm), [davidkrauser](https://github.com/davidkrauser), [devinbinnie](https://github.com/devinbinnie), [DSchalla](https://github.com/DSchalla), [Eleferen](https://translate.mattermost.com/user/Eleferen), [enahum](https://github.com/enahum), [enzowritescode](https://github.com/enzowritescode), [errotu](https://github.com/errotu), [esarafianou](https://github.com/esarafianou), [evituzas](https://translate.mattermost.com/user/evituzas), [fmartingr](https://github.com/fmartingr), [frankps](https://translate.mattermost.com/user/frankps), [fsilye](https://github.com/fsilye), [gabrieljackson](https://github.com/gabrieljackson), [hanzei](https://github.com/hanzei), [harshilsharma63](https://github.com/harshilsharma63), [hmhealey](https://github.com/hmhealey), [isacikgoz](https://github.com/isacikgoz), [jadrales](https://github.com/jadrales), [JahleelT](https://github.com/JahleelT), [jasonblais](https://github.com/jasonblais), [jeoooo](https://github.com/jeoooo), [jespino](https://github.com/jespino), [johnsonbrothers](https://github.com/johnsonbrothers), [jprusch](https://github.com/jprusch), [JulienTant](https://github.com/JulienTant), [kaakaa](https://github.com/kaakaa), [kasyap1234](https://github.com/kasyap1234), [Kshitij-Katiyar](https://github.com/Kshitij-Katiyar), [KuSh](https://github.com/KuSh), [larkox](https://github.com/larkox), [lieut-data](https://github.com/lieut-data), [lil5](https://github.com/lil5), [lucasvbeek](https://github.com/lucasvbeek), [M-ZubairAhmed](https://github.com/M-ZubairAhmed), [majo](https://translate.mattermost.com/user/majo), [marianunez](https://github.com/marianunez), [mariuskarotkis](https://translate.mattermost.com/user/mariuskarotkis), [master7](https://translate.mattermost.com/user/master7), [matt-w99](https://github.com/matt-w99), [matthew-w](https://translate.mattermost.com/user/matthew-w), [matthewbirtch](https://github.com/matthewbirtch), [melroy89](https://github.com/melroy89), [mgdelacroix](https://github.com/mgdelacroix), [mlcuchlu](https://translate.mattermost.com/user/mlcuchlu), [nickmisasi](https://github.com/nickmisasi), [panoramix360](https://github.com/panoramix360), [polinapianina](https://github.com/polinapianina), [pvev](https://github.com/pvev), [rahimrahman](https://github.com/rahimrahman), [Rajat-Dabade](https://github.com/Rajat-Dabade), [Reinkard](https://github.com/Reinkard), [Ricky-Tigg](https://github.com/Ricky-Tigg), [Roy-Orbison](https://github.com/Roy-Orbison), [sadohert](https://github.com/sadohert), [saket-dev01](https://github.com/saket-dev01), [saturninoabril](https://github.com/saturninoabril), [sbishel](https://github.com/sbishel), [Sharuru](https://github.com/Sharuru), [spirosoik](https://github.com/spirosoik), [stafot](https://github.com/stafot), [streamer45](https://github.com/streamer45), [surya2611](https://github.com/surya2611), [ThrRip](https://github.com/ThrRip), [timstott](https://github.com/timstott), [tnir\](https://translate.mattermost.com/user/tnir), [toninis](https://github.com/toninis), [vasilybels](https://translate.mattermost.com/user/vasilybels), [ViKriuVK](https://translate.mattermost.com/user/ViKriuVK), [vish9812](https://github.com/vish9812), [wiggin77](https://github.com/wiggin77), [Willyfrog](https://github.com/Willyfrog), [yasserfaraazkhan](https://github.com/yasserfaraazkhan)

(release-v10.7-feature-release)=
## Release v10.7 - [Feature Release](https://docs.mattermost.com/about/release-policy.html#release-types)

- **10.7.4, released 2025-06-18**
  - Mattermost v10.7.4 contains high severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged MS Teams plugin [v2.2.1](https://github.com/mattermost/mattermost-plugin-msteams/releases/tag/v2.2.1).
  - Pre-packaged Playbooks plugin [v1.41.1](https://github.com/mattermost/mattermost-plugin-playbooks/releases/tag/v1.41.1).
  - Pre-packaged Boards plugin version [v9.1.3](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.1.3).
  - Added support for SSO while Mattermost is embedded in an iframe [MM-63900](https://mattermost.atlassian.net/browse/MM-63900).
  - Mattermost v10.7.4 contains no database or functional changes.
- **10.7.3, released 2025-05-21**
  - Mattermost v10.7.3 contains a Critical severity level security fix. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release as soon as possible is highly recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Playbooks plugin [v2.2.0](https://github.com/mattermost/mattermost-plugin-playbooks/releases/tag/v2.2.0).
  - Fixed an issue where Team Admin permissions couldn't be changed if they were missing in **All members** section [MM-64157](https://mattermost.atlassian.net/browse/MM-64157).
  - Mattermost v10.7.3 contains no database or functional changes.
- **10.7.2, released 2025-05-12**
  - Mattermost v10.7.2 contains low to medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Mattermost v10.7.2 contains no database or functional changes.
- **10.7.1, released 2025-04-29**
  - Mattermost v10.7.1 contains a low severity level security fix. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Fixed an issue where plugins were disabled when Mattermost was embedded [MM-63507](https://mattermost.atlassian.net/browse/MM-63507).
  - Fixed an issue with post links trapping focus when hovered or focused using the keyboard [MM-62005](https://mattermost.atlassian.net/browse/MM-62005).
  - Stopped logging websocket PING events received by the server [MM-63693](https://mattermost.atlassian.net/browse/MM-63693).
  - Mattermost v10.7.1 contains no database or functional changes.
- **10.7.0, released 2025-04-16**
  - Original 10.7.0 release.

### Compatibility
 - Updated minimum Edge and Chrome versions to 132+.

### Important Upgrade Notes
 - Added a new column ``BannerInfo`` in the ``Channels`` table for storing metadata for an upcoming licensed feature. 
 - Added support for cursor-based pagination on the property architecture tables, including SQL migration to create indices. 

```{Important}
If you upgrade from a release earlier than v10.6, please read the other [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html).
```

### Improvements

#### User Interface (UI)
 - Pre-packaged Calls plugin version [v1.6.0](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.6.0). 
 - Webapp plugin loading and footer are now disabled if ``MMEMBED`` cookie is set.
 - Updated the ``marked`` package which includes full-width punctuation intervals for Unicode characters fix.
 - Added a minor change in the message priority checkbox menu item; the description width is now smaller than in previous versions.
 - Updated the library used for controlling and positioning the emoji picker.
 - Added a browser window title to the **Scheduled Posts** tab. The title is **Scheduled - <team name>**, using the same pattern as the **Drafts** tab.

#### Administration
 - Added a new System Console page called **Embedding** which allows frame ancestor domains to be specified when embedding Mattermost in other web sites. Note, ``teams.microsoft.com`` is no longer added automatically to the frame ancestors list.
 - The Channel Export plugin is removed from the transitional package list as it is now pre-packaged.
 - Removed unnecessary log messages by checking the license before calling to retrieve groups.
 - Made configuration location in the Support Packet human-readable.
 - Added advanced audit and notifications logs to the Support Packet.
 - Added log information to LDAP sync about ``include_removed_members`` option.
 - Upgraded ``react-select`` from v3.0.3 to v5.9.0.

### Bug Fixes
 - Fixed an issue with the alignment of the draft list when scheduled posts are disabled.
 - Fixed an issue where threads created by users were auto-followed on reply by the creator when they left the channel.
 - Fixed an issue where muted channels in other teams would show their mentions in the title bar.
 - Fixed an issue where messages from new channels in other teams wouldn't show up until a refresh.
 - Fixed an issue with the scrolling behavior when navigating the Direct Message list using UP/DOWN arrow keys.
 - Fixed a few minor bugs with websocket reconnection logic in the webapp.
 - Fixed an issue where DND statuses did not expire at the expiry time displayed in the app.
 - Fixed an issue where the group mentions permission was missing.
 - Fixed an issue where a system bot reply to a command entered in a thread was also posted in the channel.
 - Fixed an issue where the channel member menu could open in the wrong direction.
 - Fixed an issue where the edit post textbox sized incorrectly with the Grammarly browser extension installed.
 - Fixed an issue where onclick was missing in the channel header text, thus enabling hashtag, link, and mention clicks.
 - Fixed an issue with jobs in a High Availability environment, where two job servers would take the same job.
 - Fixed an issue where there was inconsistent behaviour on removing non-group members from group synced teams and channels.

### config.json
New setting options were added to ``config.json``. Below is a list of the additions and their default values on install. The settings can be modified in ``config.json``, or the System Console when available.

#### Changes to all plans:
 - Under ``MetricsSettings`` in ``config.json``:
    - Added ``ClientSideUserIds`` where users can set the user IDs that they want to track for client-side webapp metrics. The total number of userIDs have been capped to 5 for performance reasons, otherwise Prometheus gets overwhelmed with high label cardinality. We recommend modifying this list infrequently to ensure Prometheus performance. 
 - Under ``CacheSettings`` in ``config.json``:
    - Added ``RedisCachePrefix`` has been added which can be used to add a prefix to all Redis cache keys. 
 - Under ``ServiceSettings`` in ``config.json``:
    - Added a new configuration setting ``FrameAncestors`` to allow frame ancestor domains to be specified when embedding Mattermost in other web sites. 

#### Changes to Enterprise plans:
 - Under ``NativeAppSettings`` in ``config.json``:
    - Added new settings to enable mobile biometric authentication prompt, jailbreak / root detection and to prevent screen captures. The settings are: ``MobileEnableBiometrics`` (default: false), ``MobilePreventScreenCapture`` (default: false), ``MobileJailbreakProtection`` (default: false).
 - Added a new configuration setting ``LdapSettingsDefaultMaximumLoginAttempts``.

### API Changes
 - Added new ``pluginapi`` methods for managing groups, a new group source type called GroupSourcePluginPrefix and added a new URL parameter called include_syncable_sources to GET /api/v4/groups.
 - Added ``Client4.createPostEphemeral`` method.

### Websocket Event Changes
 - Added Custom Profile Attributes websocket support.
 - Added websocket messages to the Custom Profile Attributes operations.

### Go Version
 - v10.7 is built with Go ``v1.22.6``.

### Known Issues
 - Tooltip and highlight of icon for sidebar expansion appear after pressing **Enter** on a search [MM-63640](https://mattermost.atlassian.net/browse/MM-63640).
 - Shortcut keys to open the right-hand side from the last post in a channel are causing blue borders to be shown in the right-hand side header [MM-63562](https://mattermost.atlassian.net/browse/MM-63562).
 - Setting the license file location through an environment variable still gives the option to upload a new license through the System Console, resulting in the license being overwritten by the one set through the environment variable. See this [knowledge base article](https://support.mattermost.com/hc/en-us/articles/33911983851284-System-console-still-displays-old-license-after-uploading-a-new-one) on how to resolve this issue.
 - Searching stop words in quotation marks with Elasticsearch enabled returns more than just the searched terms.
 - Slack import through the CLI fails if email notifications are enabled.

### Contributors
 - [agarciamontoro](https://github.com/agarciamontoro), [agnivade](https://github.com/agnivade), [AlexKalopsia](https://github.com/AlexKalopsia), [amyblais](https://github.com/amyblais), [andrleite](https://github.com/andrleite), [angeloskyratzakos](https://github.com/angeloskyratzakos), [anlerandy](https://github.com/anlerandy), [Aryakoste](https://github.com/Aryakoste), [AulakhHarsh](https://github.com/AulakhHarsh), [ayush-chauhan233](https://github.com/ayush-chauhan233), [BenCookie95](https://github.com/BenCookie95), [bndn](https://github.com/bndn), [Boruus](https://github.com/Boruus), [bshumylo](https://github.com/bshumylo), [calebroseland](https://github.com/calebroseland), [capricorni](https://translate.mattermost.com/user/capricorni), [Carloswaldo](https://github.com/Carloswaldo), [CBID2](https://github.com/CBID2), [cfarrell987](https://github.com/cfarrell987), [cinlloc](https://github.com/cinlloc), [Combs7th](https://github.com/Combs7th), [cpoile](https://github.com/cpoile), [ctlaltdieliet](https://translate.mattermost.com/user/ctlaltdieliet), 
[cwarnermm](https://github.com/cwarnermm), [davidkrauser](https://github.com/davidkrauser), [DeathCamel58](https://github.com/DeathCamel58), [devinbinnie](https://github.com/devinbinnie), [DHaussermann](https://github.com/DHaussermann), [Dschoordsch](https://github.com/Dschoordsch), [Eleferen](https://translate.mattermost.com/user/Eleferen), [enahum](https://github.com/enahum), [equalsgibson](https://github.com/equalsgibson), [esarafianou](https://github.com/esarafianou), [esethna](https://github.com/esethna), [ewwollesen](https://github.com/ewwollesen), [felixerdy](https://github.com/felixerdy), [fmartingr](https://github.com/fmartingr), [frankps](https://translate.mattermost.com/user/frankps), [fsilye](https://github.com/fsilye), [gabrieljackson](https://github.com/gabrieljackson), [hanzei](https://github.com/hanzei), [harshilsharma63](https://github.com/harshilsharma63), [henrique](https://translate.mattermost.com/user/henrique), [hmhealey](https://github.com/hmhealey), [hpflatorre](https://github.com/hpflatorre), [isacikgoz](https://github.com/isacikgoz), [iyampaul](https://github.com/iyampaul), [j0794](https://github.com/j0794), [jachewz](https://github.com/jachewz), [jaehyun-ko](https://github.com/jaehyun-ko), [jasonblais](https://github.com/jasonblais), [jesperordrup](https://translate.mattermost.com/user/jesperordrup), [jespino](https://github.com/jespino), [jlandells](https://github.com/jlandells), [johnsonbrothers](https://github.com/johnsonbrothers), [jprusch](https://github.com/jprusch), [JulienTant](https://github.com/JulienTant), [kaakaa](https://github.com/kaakaa), [kayazeren](https://github.com/kayazeren), [kondo97](https://github.com/kondo97), [Kshitij-Katiyar](https://github.com/Kshitij-Katiyar), [larkox](https://github.com/larkox), [lathiat](https://github.com/lathiat), [lieut-data](https://github.com/lieut-data), [lynn915](https://github.com/lynn915), [majo](https://translate.mattermost.com/user/majo), [marianunez](https://github.com/marianunez), [master7](https://translate.mattermost.com/user/master7), [matt-w99](https://github.com/matt-w99), [matthew-w](https://translate.mattermost.com/user/matthew-w), [matthewbirtch](https://github.com/matthewbirtch), [mgdelacroix](https://github.com/mgdelacroix), [Michal](https://translate.mattermost.com/user/Michal), [moeenio](https://translate.mattermost.com/user/moeenio), [Morgansvk](https://github.com/Morgansvk), [Movion](https://github.com/Movion), [nickmisasi](https://github.com/nickmisasi), [Nityanand13](https://github.com/Nityanand13), [omerfsen](https://github.com/omerfsen), [pineoak-audio](https://github.com/pineoak-audio), [potatogim](https://translate.mattermost.com/user/potatogim), [pvev](https://github.com/pvev), [raghavaggarwal2308](https://github.com/raghavaggarwal2308), [rahimrahman](https://github.com/rahimrahman), [Reinkard](https://github.com/Reinkard), [ricardogalvao](https://translate.mattermost.com/user/ricardogalvao), [Ricky-Tigg](https://github.com/Ricky-Tigg), [robregonm](https://github.com/robregonm), [Saturate](https://github.com/Saturate), [SaurabhSharma-884](https://github.com/SaurabhSharma-884), [sbishel](https://github.com/sbishel), [stafot](https://github.com/stafot), [streamer45](https://github.com/streamer45), [sumitbhanushali](https://github.com/sumitbhanushali), [svelle](https://github.com/svelle), [ThrRip](https://github.com/ThrRip), [tnir](https://github.com/tnir), [trokar](https://translate.mattermost.com/user/trokar), [wiersgallak](https://github.com/wiersgallak), [wiggin77](https://github.com/wiggin77), [Willyfrog](https://github.com/Willyfrog), [yasserfaraazkhan](https://github.com/yasserfaraazkhan)

(release-v10.6-feature-release)=
## Release v10.6 - [Feature Release](https://docs.mattermost.com/about/release-policy.html#release-types)

- **10.6.6, released 2025-05-21**
  - Mattermost v10.6.6 contains a Critical severity level security fix. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release as soon as possible is highly recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Playbooks plugin [v2.2.0](https://github.com/mattermost/mattermost-plugin-playbooks/releases/tag/v2.2.0).
  - Mattermost v10.6.6 contains no database or functional changes.
- **10.6.5, released 2025-05-15**
  - Added support for AES-256-GCM encryption in SAML [MM-64222](https://mattermost.atlassian.net/browse/MM-64222).
  - Fixed an issue where Team Admin permissions couldn't be changed if they were missing in "All members" section [MM-64157](https://mattermost.atlassian.net/browse/MM-64157).
  - Mattermost v10.6.5 contains no database or functional changes.
- **10.6.4, released 2025-05-12**
  - Mattermost v10.6.4 contains low to medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Mattermost v10.6.4 contains no database or functional changes.
- **10.6.3, released 2025-04-29**
  - Mattermost v10.6.3 contains low to medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Mattermost v10.6.3 contains no database or functional changes.
- **10.6.2, released 2025-04-15**
  - Mattermost v10.6.2 contains low to medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Stopped logging websocket PING events received by the server [MM-63693](https://mattermost.atlassian.net/browse/MM-63693).
  - Fixed an issue with post links trapping focus when hovered or focused using the keyboard [MM-62005](https://mattermost.atlassian.net/browse/MM-62005).
  - Mattermost v10.6.2 contains no database or functional changes.
- **10.6.1, released 2025-03-17**
  - Fixed an issue with jobs in an High Availability environment, where two job servers would take the same job [MM-63314](https://mattermost.atlassian.net/browse/MM-63314).
  - Pre-packaged Calls plugin version [v1.5.2](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.5.2).
  - Mattermost v10.6.1 contains the following functional changes:
      - Added a new System Console page called ``Embedding`` which allows frame ancestor domains to be specified when embedding Mattermost in other web sites. Note, ``teams.microsoft.com`` is no longer added automatically to the frame ancestors list. Added a new configuration setting ``FrameAncestors`` [MM-63327](https://mattermost.atlassian.net/browse/MM-63327).
- **10.6.0, released 2025-03-14**
  - Original 10.6.0 release.

### Important Upgrade Notes
 - Support for PostgreSQL v11 and v12 have been removed. The new minimum PostgreSQL version is v13+. See the [minimum supported PostgreSQL version policy](https://docs.mattermost.com/deploy/software-hardware-requirements.html#minimum-postgresql-database-support-policy) documentation for details.
 - Migration times: On a system with 12M posts, and 1M fileinfo entries, the migration takes 15s. This migration is non-locking. Note that there is no migration for MySQL deployments because this optimization is only applicable for PostgreSQL.

```{Important}
If you upgrade from a release earlier than v10.5, please read the other [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html).
```

### Improvements

#### User Interface (UI)
 - Pre-packaged Boards plugin version [v9.1.1](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.1.1). 
 - Pre-packaged Playbooks plugin version [v2.1.1](https://github.com/mattermost/mattermost-plugin-playbooks/releases/tag/v2.1.1).
 - Pre-packaged Copilot plugin version [v1.1.1](https://github.com/mattermost/mattermost-plugin-ai/releases/tag/v1.1.1).
 - Pre-packaged MS Teams plugin version [v2.1.1](https://github.com/mattermost/mattermost-plugin-msteams/releases/tag/v2.1.1).
 - Pre-packaged Jira plugin version [v4.2.1](https://github.com/mattermost/mattermost-plugin-jira/releases/tag/v4.2.1).
 - Upgraded Ukrainian language to official.

#### Administration
 - System Console statistics now perform faster on PostgreSQL. The ``MaxUsersForStatistics`` configuration setting now only disables the **User counts with posts** chart, while all other stats remain unaffected. The other stats remain unaffected because that configuration value is no longer needed to disable the other queries since they are always fast now. Post and file counts update daily, so they may not always reflect real-time data. Advanced stats, such as line charts and plugin data, are now hidden until clicked, reducing load time. No performance improvements apply to MySQL since it's scheduled for full deprecation in v11. We recommend migrating to PostgreSQL for better performance and long-term support. The migration process for PostgreSQL is quick (around 15 seconds for large systems) and non-blocking. If you're on MySQL, no migration is needed, but transitioning to PostgreSQL is strongly encouraged.
 - Unlicensed server limits have been updated: a soft limit of 2500 users now results in a banner notification visible by admins, and a 5K hard limit that prevents the creation or activation of users until the user count is reduced below the hard limit.
 - Removed the automatic Elasticsearch/OpenSearch channel index schema check. As a result, admins will no longer receive Direct Message alerts to notify that their ``elasticsearch`` channel index is out of date.

### Bug Fixes
 - Fixed an issue where the email address in Mattermost would not get updated if the one in SAML changed. 
 - Fixed an issue where deleted messages would still show thread replies in the channel. 
 - Fixed an error that could occur when navigating away from the threads screen. 
 - Fixed an issue where INFO level logging for ``DoActionRequest POST`` requests was missing. 
 - Fixed an issue where users did not have the ability to toggle the switcher menu in the global header using the **SPACE** and **ENTER** keys while the product branding was in focus. 
 - Fixed "An error has occurred" bar being shown with developer mode disabled. 
 - Fixed an issue where deleted threads would get stuck in the thread viewer. 
 - Fixed an issue where the channel file count was incorrect due to files not actually being submitted as part of a post. 
 - Fixed a crash issue in the integration action system. 
 - Fixed an issue where a currently selected thread was shown in the **Unreads** pane.
 - Fixed an issue with mmctl preventing the logging of a harmless debug-level "error". 
 - Fixed an issue where the unread count in your team sidebar may be out of sync when following/unfollowing threads. 
 - Fixed an issue with Bulk Export: Exports will no longer stop when they encounter a missing file. 

### config.json
New setting options were added to ``config.json``. Below is a list of the additions and their default values on install. The settings can be modified in ``config.json``, or the System Console when available.

#### Changes to all plans:
- Under ``ServiceSettings`` in ``conig.json``:
  - A new configuration setting ``EnableWebHubChannelIteration`` was added, which allows a user to control the performance of websocket broadcasting. By default, this setting is turned off. If it is turned on, it improves the websocket broadcasting performance at the expense of poor performance when users join/leave a channel. We don't recommended turning this on unless you have at least 200,000 concurrent users actively using Mattermost.
- Removed ``EnableOpenTracing`` to remove the unused ``opentracing`` support. 

### API Changes
 - Added audit logging to the ``SearchPosts`` API.
 - Added a ``metrics`` tag to ``client_perf`` endpoint.

### Open Source Components
 - Added and removed several components.

### Go Version
 - v10.6 is built with Go ``v1.22.6``.

### Known Issues
 - Setting the license file location through an environment variable still gives the option to upload a new license through the System Console, resulting in the license being overwritten by the one set through the environment variable. See this [knowledge base article](https://support.mattermost.com/hc/en-us/articles/33911983851284-System-console-still-displays-old-license-after-uploading-a-new-one) on how to resolve this issue.
 - Searching stop words in quotation marks with Elasticsearch enabled returns more than just the searched terms.
 - Slack import through the CLI fails if email notifications are enabled.

### Contributors
 - [agarciamontoro](https://github.com/agarciamontoro), [agnivade](https://github.com/agnivade), [amyblais](https://github.com/amyblais), [andrleite](https://github.com/andrleite), [angeloskyratzakos](https://github.com/angeloskyratzakos), [Aryakoste](https://github.com/Aryakoste), [ayush-chauhan233](https://github.com/ayush-chauhan233), [BenCookie95](https://github.com/BenCookie95), [bshumylo](https://github.com/bshumylo), [calebroseland](https://github.com/calebroseland), [cpoile](https://github.com/cpoile), [crspeller](https://github.com/crspeller), [ctlaltdieliet](https://github.com/ctlaltdieliet), [cwarnermm](https://github.com/cwarnermm), [darkcircle](https://translate.mattermost.com/user/darkcircle), [davidkrauser](https://github.com/davidkrauser), [devinbinnie](https://github.com/devinbinnie), [dgwhited](https://github.com/dgwhited), [Eleferen](https://translate.mattermost.com/user/Eleferen), [enahum](https://github.com/enahum), [enzowritescode](https://github.com/enzowritescode), [equalsgibson](https://github.com/equalsgibson), [esarafianou](https://github.com/esarafianou), [fmartingr](https://github.com/fmartingr), [frankps](https://translate.mattermost.com/user/frankps), [fsilye](https://github.com/fsilye), [gabrieljackson](https://github.com/gabrieljackson), [hanzei](https://github.com/hanzei), [harshilsharma63](https://github.com/harshilsharma63), [henrique](https://translate.mattermost.com/user/henrique), [hereje](https://github.com/hereje), [hmhealey](https://github.com/hmhealey), [hpflatorre](https://github.com/hpflatorre), [ifoukarakis](https://github.com/ifoukarakis), [isacikgoz](https://github.com/isacikgoz), [jespino](https://github.com/jespino), [jlandells](https://github.com/jlandells), [johnsonbrothers](https://github.com/johnsonbrothers), [jprusch](https://github.com/jprusch), [JulienTant](https://github.com/JulienTant), [jwilander](https://github.com/jwilander), [kaakaa](https://github.com/kaakaa), [kayazeren](https://github.com/kayazeren), [Kshitij-Katiyar](https://github.com/Kshitij-Katiyar), [KuSh](https://github.com/KuSh), [larkox](https://github.com/larkox), [lieut-data](https://github.com/lieut-data), [liul8258](https://github.com/liul8258), [M-ZubairAhmed](https://github.com/M-ZubairAhmed), [majo](https://translate.mattermost.com/user/majo), [marianunez](https://github.com/marianunez), [master7](https://translate.mattermost.com/user/master7), [matt-w99](https://github.com/matt-w99), [matthew-w](https://translate.mattermost.com/user/matthew-w), [mgdelacroix](https://github.com/mgdelacroix), [Morgansvk](https://github.com/Morgansvk), [mvitale1989](https://github.com/mvitale1989), [natalie-hub](https://github.com/natalie-hub), [nathanaelhoun](https://github.com/nathanaelhoun), [NCPSNetworks](https://github.com/NCPSNetworks), [nickmisasi](https://github.com/nickmisasi), [panoramix360](https://github.com/panoramix360), [pvev](https://github.com/pvev), [rahimrahman](https://github.com/rahimrahman), [Rajat-Dabade](https://github.com/Rajat-Dabade), [Reinkard](https://github.com/Reinkard), [Ricky-Tigg](https://github.com/Ricky-Tigg), [robregonm](https://github.com/robregonm), [SaurabhSharma-884](https://github.com/SaurabhSharma-884), [sbishel](https://github.com/sbishel), [SorenHolm](https://translate.mattermost.com/user/SorenHolm), [stafot](https://github.com/stafot), [streamer45](https://github.com/streamer45), [svelle](https://github.com/svelle), [ThrRip](https://github.com/ThrRip), [tnir](https://translate.mattermost.com/user/tnir), [toninis](https://github.com/toninis), [Victor-Nyagudi](https://github.com/Victor-Nyagudi), [wiersgallak](https://github.com/wiersgallak), [wiggin77](https://github.com/wiggin77), [Willyfrog](https://github.com/Willyfrog), [willypuzzle](https://github.com/willypuzzle), [yasserfaraazkhan](https://github.com/yasserfaraazkhan)

(release-v10.5-extended-support-release)=
## Release v10.5 - [Extended Support Release](https://docs.mattermost.com/about/release-policy.html#release-types)

- **10.5.9, released 2025-07-22**
  - Mattermost v10.5.9 contains low to medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release as soon as possible is highly recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Boards plugin version [v9.1.4](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.1.4).
  - Pre-packaged Agents plugin [v1.2.4](https://github.com/mattermost/mattermost-plugin-agents/releases/tag/v1.2.4).
  - Pre-packaged Calls plugin [v1.9.2](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.9.2).
  - Fixed an issue where overridden webhook usernames did not appear in replies when Threaded Discussions were disabled [MM-63564](https://mattermost.atlassian.net/browse/MM-63564).
  - Removed redux selector's telemetry [MM-63794](https://mattermost.atlassian.net/browse/MM-63794).
  - Mattermost v10.5.9 contains no database or functional changes.
- **10.5.8, released 2025-06-18**
  - Mattermost v10.5.8 contains a high severity level security fix. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Fixed an issue where unreads from deleted teams would display in the titlebar/Desktop App [MM-63933](https://mattermost.atlassian.net/browse/MM-63933).
  - Pre-packaged Playbooks plugin [v1.41.1](https://github.com/mattermost/mattermost-plugin-playbooks/releases/tag/v1.41.1).
  - Pre-packaged Boards plugin version [v9.1.3](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.1.3).
  - Mattermost v10.5.8 contains no database or functional changes.
- **10.5.7, released 2025-05-27**
  - Mattermost v10.5.7 contains a high severity level security fix. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Fixed possible deadlocks when updating ``SidebarCategories`` and ``SidebarChannels`` tables [MM-63923](https://mattermost.atlassian.net/browse/MM-63923).
  - Pre-packaged MS Teams plugin [v2.2.1](https://github.com/mattermost/mattermost-plugin-msteams/releases/tag/v2.2.1).
  - Mattermost v10.5.7 contains no database or functional changes.
- **10.5.6, released 2025-05-21**
  - Mattermost v10.5.6 contains a Critical severity level security fix. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release as soon as possible is highly recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Playbooks plugin [v2.2.0](https://github.com/mattermost/mattermost-plugin-playbooks/releases/tag/v2.2.0).
  - Pre-packaged Calls plugin [v1.7.1](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.7.1).
  - Fixed an issue where Team Admin permissions couldn't be changed if they were missing in **All members** section [MM-64157](https://mattermost.atlassian.net/browse/MM-64157).
  - Mattermost v10.5.6 contains no database or functional changes.
- **10.5.5, released 2025-05-09**
  - Mattermost v10.5.5 contains low to medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Mattermost v10.5.5 contains the following database changes:
    - A new index to the ``CategoryId`` column in ``SidebarChannels`` table was added to improve query performance. No database downtime is expected for this upgrade. It takes around 2s to add the index on a table with 1.2M rows for PostgreSQL, and it takes around 5s on MySQL on a table with 300K rows. The migrations are fully backwards-compatible and no table locks or existing operations on the table are impacted by this upgrade. Zero downtime is expected when upgrading to this release. The SQL queries included are ``CREATE INDEX idx_sidebarchannels_categoryid ON SidebarChannels(CategoryId);`` for MYSQL and ``CREATE INDEX CONCURRENTLY IF NOT EXISTS idx_sidebarchannels_categoryid ON sidebarchannels(categoryid);`` for PostgreSQL. 
- **10.5.4, released 2025-04-29**
  - Mattermost v10.5.4 contains low to medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Fixed an issue where **Recent Mentions** showed incorrect results for custom notification keywords containing hyphens [MM-63582](https://mattermost.atlassian.net/browse/MM-63582).
  - Fixed an issue with post links trapping focus when hovered or focused using the keyboard [MM-62005](https://mattermost.atlassian.net/browse/MM-62005).
  - Mattermost v10.5.4 contains no database or functional changes.
- **10.5.3, released 2025-04-15**
  - Mattermost v10.5.3 contains low to medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Metrics plugin version [v0.6.0](https://github.com/mattermost/mattermost-plugin-metrics/releases/tag/v0.6.0).
  - Stopped logging websocket PING events received by the server [MM-63693](https://mattermost.atlassian.net/browse/MM-63693).
  - Mattermost v10.5.3 contains no database or functional changes.
- **10.5.2, released 2025-03-17**
  - Mattermost v10.5.2 contains low to high severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged MS Teams plugin version [v2.1.1](https://github.com/mattermost/mattermost-plugin-msteams/releases/tag/v2.1.1).
  - Pre-packaged Jira plugin version [v4.2.1](https://github.com/mattermost/mattermost-plugin-jira/releases/tag/v4.2.1).
  - Pre-packaged Calls plugin version [v1.5.2](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.5.2).
  - Mattermost v10.5.2 contains no database or functional changes.
- **10.5.1, released 2025-02-19**
  - Mattermost v10.5.1 contains low to high severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Boards plugin version [v9.1.1](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.1.1).
  - Pre-packaged Playbooks plugin version [v2.1.1](https://github.com/mattermost/mattermost-plugin-playbooks/releases/tag/v2.1.1).
  - Fixed an issue in Compliance Exports whereby a missing file attachment in S3 could prevent the export run from completing [MM-62527](https://mattermost.atlassian.net/browse/MM-62527).
  - Mattermost v10.5.1 contains the following functional changes:
      - A new configuration setting ``ServiceSettings.EnableWebHubChannelIteration`` was added which allows a user to control the performance of websocket broadcasting. By default, this setting is turned off. If it is turned on, it improves the websocket broadcasting performance at the expense of poor performance when users join/leave a channel. It is not recommended to turn it on unless you have atleast 200,000 concurrent users actively using Mattermost.
- **10.5.0, released 2025-02-14**
  - Original 10.5.0 release.

### Compatibility
 - Updated minimum Safari version to 17.4+ and minimum Firefox version to 119+.

### Important Upgrade Notes
 - Mattermost versions v10.5.0 and v10.5.1 include a bundled Jira plugin (v4.2.0) that contains a bug which may cause plugin configuration settings to disappear. We strongly advise against upgrading to these versions to avoid potential disruption.  
If you have already upgraded to v10.5.0 or v10.5.1, we recommend updating the Jira plugin to version v4.2.1, or preferably, upgrading both Mattermost and the Jira plugin to their latest available versions.
 - v10.5 introduces Property System Architecture schema migration. See the [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html) for details.
 - The Compliance Export system has been overhauled. See the [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html) for details.
 - The Mattermost server has stopped supporting manual plugin deployment. Plugins were deployed manually when an administrator or some deployment automation copies the contents of a plugin bundle into the server's working directory. If a manual or automated deployment workflow is still required, administrators can instead prepackage the plugin bundles. See more details in [this forum post](https://forum.mattermost.com/t/deprecation-notice-manual-plugin-deployment/21192).
 - Mattermost has stopped official Mattermost server builds for the Microsoft Windows operating system. Administrators should migrate existing Mattermost server installations to use the official Linux builds. See more details in [this forum post](https://forum.mattermost.com/t/deprecation-notice-server-builds-for-microsoft-windows/21498).

### Breaking Changes
- The internal workings of the `PluginLinkComponent` in the web app have been changed to unmount link tooltips from the DOM by default, significantly improving performance. Plugins that register link tooltips using `registerLinkTooltipComponent` will experience changes in how tooltip components are managed—they are now only mounted when a link is hovered over or focused. As a result, plugins may need to update their components to properly handle mounting and unmounting scenarios. For example, changes were made in [mattermost-plugin-jira](https://github.com/mattermost/mattermost-plugin-jira/pull/1145), where componentDidUpdate lifecycle hook was replaced with componentDidMount. If your plugin’s tooltip component is a functional React component, there is a high chance that this behavior will be handled automatically, as it would be managed by useEffect with an empty dependency array.

```{Important}
If you upgrade from a release earlier than v10.3, please read the other [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html).
```

### Improvements

#### User Interface (UI)
 - Pre-packaged Boards plugin [v9.1.0](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.1.0).
 - Pre-packaged Calls plugin [v1.5.1](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.5.1).
 - Pre-packaged MS Teams plugin [v2.1.0](https://github.com/mattermost/mattermost-plugin-msteams/releases/tag/v2.1.0).
 - Pre-packaged Channel Export plugin [v1.2.1](https://github.com/mattermost/mattermost-plugin-channel-export/releases/tag/v1.2.1).
 - Pre-packaged Jira plugin [v4.2.0](https://github.com/mattermost/mattermost-plugin-jira/releases/tag/v4.2.0).
 - Added the ability to modify post attachments during edit.
 - The channel bookmarks bar is now hidden when there are no bookmarks in the channel. Bookmarks can now be added from the channel menu.
 - Removed the video from the onboarding checklist.
 - Improved accessibility throughout the webapp by fixing several issues around keyboard navigation and screen reader focused on modals, right-hand side and core chat functionality. 

#### Administration
 - Added the migrations, store layer and service for the Property System Architecture.
 - Added Custom Profile Attributes, an experimental Enterprise-only feature. This feature is disabled by default. To enable this feature, set the feature flag `CustomProfileAttributes`. Once enabled, administrators can access the System Properties section in the System Console to create and manage custom user profile fields. The initial release supports text fields only.
 - Added the Custom Profile Attribute fields store, app and API endpoints.
 - Introduced V2 of the Support Packet, containing improvement diagnosis information for high-availability deployments.
 - Added a new ``Fallback`` field to ``PluginSettingsSection`` that controls whether the settings defined under the section should still render as fallback when the plugin is disabled.
 - Updated the library used for tooltips throughout the app to fix a memory leak.
 - Reduced the volume of unnecessary debug logs generated during scheduled post job execution.
 - Removed ``form-data`` from @mattermost/client.

### Bug Fixes
 - Fixed archived filter behavior in System Console > User Management > Channels to restore the ability to exclude archived channels.
 - Fixed an issue where DMs/GMs with a `DeleteAt` non-zero value in the database might cause issues with several APIs.
 - Fixed an issue where the team sidebar's mention count could be out of sync with the thread count.
 - Fixed an issue where replies with props could not be imported.
 - Fixed an issue where ``pluginapi.store.GetReplicaDB`` returned nil if masterDB was not initialized.
 - Fixed an issue in ``SqlPostStore.PermanentDeletebyUser`` where no error was returned when 10K posts were exceeded.
 - Fixed an issue where a channel would no longer be exported for Bulk Export workflow if any of the users of a Direct or Group Message channel were permanently deleted.
 - Fixed an issue where the scroll position reset when custom emojis were requested.
 - Fixed a panic during LDAP synchronization.
 - Fixed an issue where the bulk export retention job would accidentally delete non-bulk export files and directories.
 - Fixed an issue where archived channels were not searchable with Elasticsearch/OpenSearch if ``TeamSettings.ExperimentalViewArchivedChannels`` was enabled. If there are old channels which were archived before a bulk index was run, users would need to purge indexes, and do bulk index again. Because those old archived channels are removed from the index when a bulk index is run.

### config.json
New setting options were added to ``config.json``. Below is a list of the additions and their default values on install. The settings can be modified in ``config.json``, or the System Console when available.

#### Changes to Enterprise plans:
 - Under ``essageExportSettings`` in ``config.json``:
   - Added ``ComplianceExportDirectoryFormat``, ``ComplianceExportPath``, ``ComplianceExportPathCLI``, ``ComplianceExportChannelBatchSizeDefault``, and ``ComplianceExportChannelHistoryBatchSizeDefault`` for compliance export overhaul.

### API Changes
 - ``GetUsersInChannelDuring`` now accepts a slice; added ``GetChannelsWithActivityDuring``.
 - Two new boolean query parameters were added to the ``api/v4/config`` endpoint:
    - ``remove_defaults`` (filters out default values).
    - ``remove_masked`` (removes masked fields). 

### Go Version
 - v10.5 is built with Go ``v1.22.6``.

### Known Issues
 - Setting the license file location through an envvar still gives the option to upload a new license through the System Console, resulting in the license being overwritten by the one set through the envvar. See this [knowledge base article](https://support.mattermost.com/hc/en-us/articles/33911983851284-System-console-still-displays-old-license-after-uploading-a-new-one) on how to resolve this issue.
 - Searching stop words in quotation marks with Elasticsearch enabled returns more than just the searched terms.
 - Slack import through the CLI fails if email notifications are enabled.

### Contributors
 - [agarciamontoro](https://github.com/agarciamontoro), [agardelein](https://github.com/agardelein), [agnivade](https://github.com/agnivade), [amyblais](https://github.com/amyblais), [andrleite](https://github.com/andrleite), [angeloskyratzakos](https://github.com/angeloskyratzakos), [Aryakoste](https://github.com/Aryakoste), [asaadmahmood](https://github.com/asaadmahmood), [AulakhHarsh](https://github.com/AulakhHarsh), [ayush-chauhan233](https://github.com/ayush-chauhan233), [BenCookie95](https://github.com/BenCookie95), [bshumylo](https://translate.mattermost.com/user/bshumylo), [calebroseland](https://github.com/calebroseland), [code1492](https://github.com/code1492), [cpoile](https://github.com/cpoile), [crspeller](https://github.com/crspeller), [ctlaltdieliet](https://translate.mattermost.com/user/ctlaltdieliet), [cwarnermm](https://github.com/cwarnermm), [devinbinnie](https://github.com/devinbinnie), [dmanpearl](https://github.com/dmanpearl), [Dschoordsch](https://github.com/Dschoordsch), [ebuildy](https://github.com/ebuildy), [Eleferen](https://translate.mattermost.com/user/Eleferen), [emmapeel2](https://github.com/emmapeel2), [enahum](https://github.com/enahum), [enzowritescode](https://github.com/enzowritescode), [esarafianou](https://github.com/esarafianou), [fmartingr](https://github.com/fmartingr), [frankps](https://translate.mattermost.com/user/frankps), [fsilye](https://github.com/fsilye), [fume4mattermost](https://github.com/fume4mattermost), [gabrieljackson](https://github.com/gabrieljackson), [hannaparks](https://github.com/hannaparks), [hanzei](https://github.com/hanzei), [harshilsharma63](https://github.com/harshilsharma63), [henrique](https://translate.mattermost.com/user/henrique), [hmhealey](https://github.com/hmhealey), [Honsei901](https://github.com/Honsei901), [hpflatorre](https://github.com/hpflatorre), [ifoukarakis](https://github.com/ifoukarakis), [isacikgoz](https://github.com/isacikgoz), [jespino](https://github.com/jespino), [johnsonbrothers](https://github.com/johnsonbrothers), [jprusch](https://github.com/jprusch), [juliemanalo](https://github.com/juliemanalo), [JulienTant](https://github.com/JulienTant), [jure](https://translate.mattermost.com/user/jure), [jwilander](https://github.com/jwilander), [kaakaa](https://github.com/kaakaa), [kasyap1234](https://github.com/kasyap1234), [kayazeren](https://translate.mattermost.com/user/kayazeren), [kondo97](https://github.com/kondo97), [Kshitij-Katiyar](https://github.com/Kshitij-Katiyar), [larkox](https://github.com/larkox), [lieut-data](https://github.com/lieut-data), [lynn915](https://github.com/lynn915), [M-ZubairAhmed](https://github.com/M-ZubairAhmed), [majo](https://translate.mattermost.com/user/majo), [marianunez](https://github.com/marianunez), [master7](https://translate.mattermost.com/user/master7), [matthewbirtch](https://github.com/matthewbirtch), [MattSilvaa](https://github.com/MattSilvaa), [mgdelacroix](https://github.com/mgdelacroix), [Morgansvk](https://github.com/Morgansvk), [mvitale1989](https://github.com/mvitale1989), [NadavTasher](https://github.com/NadavTasher), [narutoxboy](https://translate.mattermost.com/user/narutoxboy), [NCPSNetworks](https://github.com/NCPSNetworks), [nickmisasi](https://github.com/nickmisasi), [otbutz](https://github.com/otbutz), [pvev](https://github.com/pvev), [rahimrahman](https://github.com/rahimrahman), [Rajat-Dabade](https://github.com/Rajat-Dabade), [Reinkard](https://github.com/Reinkard), [robregonm](https://github.com/robregonm), [sarthak0714](https://github.com/sarthak0714), [saturninoabril](https://github.com/saturninoabril), [SaurabhSharma-884](https://github.com/SaurabhSharma-884), [sbishel](https://github.com/sbishel), [Sharuru](https://github.com/Sharuru), [stafot](https://github.com/stafot), [streamer45](https://github.com/streamer45), [svelle](https://github.com/svelle), [ThrRip](https://github.com/ThrRip), [toninis](https://github.com/toninis), [tormi](https://translate.mattermost.com/user/tormi), [uday-rana](https://github.com/uday-rana), [unode](https://github.com/unode), [varghesejose2020](https://github.com/varghesejose2020), [Victor-Nyagudi](https://github.com/Victor-Nyagudi), [vish9812](https://github.com/vish9812), [wetneb](https://github.com/wetneb), [wiggin77](https://github.com/wiggin77), [Willyfrog](https://github.com/Willyfrog), [willypuzzle](https://github.com/willypuzzle), [X1Vi](https://github.com/X1Vi), [yasserfaraazkhan](https://github.com/yasserfaraazkhan)

(release-v10.4-feature-release)=
## Release v10.4 - [Feature Release](https://docs.mattermost.com/about/release-policy.html#release-types)

- **10.4.5, released 2025-04-15**
  - Mattermost v10.4.5 contains low to medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Stopped logging websocket PING events received by the server [MM-63693](https://mattermost.atlassian.net/browse/MM-63693).
  - Mattermost v10.4.5 contains no database or functional changes.
- **10.4.4, released 2025-03-17**
  - Mattermost v10.4.4 contains low to high severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Calls plugin version [v1.5.2](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.5.2).
  - Mattermost v10.4.4 contains no database or functional changes.
- **10.4.3, released 2025-02-19**
  - Mattermost v10.4.3 contains low to high severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Boards plugin version [v9.1.1](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.1.1).
  - Pre-packaged Playbooks plugin version [v2.1.1](https://github.com/mattermost/mattermost-plugin-playbooks/releases/tag/v2.1.1).
  - Fixed an issue in Compliance Exports whereby a missing file attachment in S3 could prevent the export run from completing [MM-62527](https://mattermost.atlassian.net/browse/MM-62527).
  - Fixed an issue where the bulk export retention job could accidentally delete non-bulk export files and directories [MM-62527](https://mattermost.atlassian.net/browse/MM-62527).
  - Mattermost v10.4.3 contains the following functional changes:
      - A new configuration setting ``ServiceSettings.EnableWebHubChannelIteration`` was added which allows a user to control the performance of websocket broadcasting. By default, this setting is turned off. If it is turned on, it improves the websocket broadcasting performance at the expense of poor performance when users join/leave a channel. It is not recommended to turn it on unless you have atleast 200,000 concurrent users actively using Mattermost.
- **10.4.2, released 2025-01-22**
  - Mattermost v10.4.2 contains critical severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Boards plugin [v9.0.5](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.0.5).
  - Pre-packaged Channel Export plugin [v1.2.1](https://github.com/mattermost/mattermost-plugin-channel-export/releases/tag/v1.2.1).
  - Fixed a panic during LDAP synchronization [MM-61239](https://mattermost.atlassian.net/browse/MM-61239).
  - Fixed an issue with webhook attachment button styles [MM-62400](https://mattermost.atlassian.net/browse/MM-62400).
  - Mattermost v10.4.2 contains no database or functional changes.
- **10.4.1, released 2025-01-16**
  - Fixed errors logged by performance telemetry due to certain browser extensions [MM-62371](https://mattermost.atlassian.net/browse/MM-62371).
  - Fixed an issue with insertion errors to ``LinkMetadata`` table.
  - Mattermost v10.4.1 contains no database or functional changes.
- **10.4.0, released 2025-01-16**
  - Original 10.4.0 release.

```{Important}
If you upgrade from a release earlier than v10.3, please read the other [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html).
```

### Improvements

#### User Interface (UI)
 - Pre-packaged Calls plugin [v1.4.0](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.4.0).
 - Pre-packaged Boards plugin [v9.0.2](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.0.2).
 - Improved the handling of Thai script in search terms.
 - Added tooltips to the buttons shown in the channel info in the right pane.
 - Downgraded Spanish language to Alpha.
 - Removed the feature to import themes from Slack.

#### Administration
 - Redis is now available as an alternative cache backend for all Enterprise customers. It can be leveraged to run Mattermost at a very high scale.
 - Plugins are now allowed to add Support Packet data without user interface elements.
 - Improved the detection of the mobile app operating system as stored in the **Sessions** table.

### Bug Fixes
 - Fixed an issue where imported replies were missing their reactions.
 - Fixed an issue with how links in Markdown headings are displayed in the Threads list.
 - Fixed an issue where marking a channel as read wouldn't persist through a refresh.
 - Fixed a warning in the Support Packet about an unreadable LDAP server even if LDAP was disabled.
 - Fixed an issue where multiple timezones were highlighted when selecting certain timezones.
 - Fixed an issue where unread messages on other teams would not appear after the application reconnected to the server.
 - Fixed an issue where the scrollbar was not clickable when there was a toaster.
 - Fixed an issue when pressing **Page Up** or **Page Down** on a long message (scrollable) with the right sidebar open.
 - Fixed an issue with incorrect reporting in the **Server Updates** section in **System Console > Workspace Optimizations**.
 - Fixed an issue where EXIF rotated image previews did not have the correct size.
 - Fixed an issue where the search input field in the emoji picker did not accept uppercase letters.
 - Fixed an issue where imported replies were missing their reactions.
 - Fixed an issue where System Administrators could not pull posts from Direct Message channels that they were not in.
 - Fixed an issue by restoring System Administrator access to Direct and Group Messages without being a member.

### config.json
New setting options were added to ``config.json``. Below is a list of the additions and their default values on install. The settings can be modified in ``config.json``, or the System Console when available.

#### Changes to all plans:
- Under ``LocalizationSettings`` in ``config.json``:
  - Added a new ``EnableExperimentalLocales`` configuration setting that controls whether to allow the selection of experimental (e.g., in progress) languages.

#### Changes to Enterprise plans:
 - Under ``CacheSettings`` in ``config.json``:
   - Added ``CacheType``: This can be either ``lru`` or ``redis``. ``lru`` is the default choice which will use the in-memory cache store that we use currently.
   - Added ``RedisAddress``: The hostname of the Redis host.
   - Added ``RedisPassword``: The password of the Redis host (can be left blank if there is no password).
   - Added ``RedisDB``: The database of the Redis host. Typically ``0``.
   - Added ``DisableClientCache``: This can be set to ``true`` if you decide to disable the client-side cache of Redis. Typically there is no need to do this in production, and this is mainly used as a test option.
 - Under ``FileSettings`` in ``config.json``:
   - Added new ``AmazonS3StorageClass`` and ``ExportAmazonS3StorageClass``, both default to ``""`` to preserve the current behavior. Administrators may configure this storage class to the storage class required by their S3 solution.

### API Changes
 - Added a new query string to exclude threads that are not part of the team ``GET api/v4/users/{user_id:[A-Za-z0-9]+}/teams/{team_id:[A-Za-z0-9]+}/threads``.

### Websocket Event Changes
 - Added a new ``server_hostname`` field to the websocket ``HELLO`` event.

### Go Version
 - v10.4 is built with Go ``v1.22.6``.

### Known Issues
 - Setting the license file location through an envvar still gives the option to upload a new license through the System Console, resulting in the license being overwritten by the one set through the envvar. See this [knowledge base article](https://support.mattermost.com/hc/en-us/articles/33911983851284-System-console-still-displays-old-license-after-uploading-a-new-one) on how to resolve this issue.
 - Searching stop words in quotation marks with Elasticsearch enabled returns more than just the searched terms.
 - Slack import through the CLI fails if email notifications are enabled.

### Contributors
 - [agarciamontoro](https://github.com/agarciamontoro), [agnivade](https://github.com/agnivade), [akbarkz](https://translate.mattermost.com/user/akbarkz), [amyblais](https://github.com/amyblais), [and-ri](https://github.com/and-ri), [andreabia](https://translate.mattermost.com/user/andreabia), [andrleite](https://github.com/andrleite), [angeloskyratzakos](https://github.com/angeloskyratzakos), [Aryakoste](https://github.com/Aryakoste), [AulakhHarsh](https://github.com/AulakhHarsh), [ayush-chauhan233](https://github.com/ayush-chauhan233), [BenCookie95](https://github.com/BenCookie95), [calebroseland](https://github.com/calebroseland), [callmeott](https://github.com/callmeott), [catalintomai](https://github.com/catalintomai), [creeper-0910](https://github.com/creeper-0910), [crspeller](https://github.com/crspeller), [ctlaltdieliet](https://github.com/ctlaltdieliet), [cwarnermm](https://github.com/cwarnermm), [davidkrauser](https://github.com/davidkrauser), [Destrosvet](https://translate.mattermost.com/user/Destrosvet), [devinbinnie](https://github.com/devinbinnie), [DHaussermann](https://github.com/DHaussermann), [Eleferen](https://translate.mattermost.com/user/Eleferen), [enahum](https://github.com/enahum), [enzowritescode](https://github.com/enzowritescode), [esarafianou](https://github.com/esarafianou), [esethna](https://github.com/esethna), [ewwollesen](https://github.com/ewwollesen), [fmartingr](https://github.com/fmartingr), [frankps](https://translate.mattermost.com/user/frankps), [fsilye](https://github.com/fsilye), [fume4mattermost](https://github.com/fume4mattermost), [fxnm](https://github.com/fxnm), [gabrielctn](https://github.com/gabrielctn), [gabrieljackson](https://github.com/gabrieljackson), [gabsfrancis](https://translate.mattermost.com/user/gabsfrancis), [Gesare5](https://github.com/Gesare5), [Haliax](https://translate.mattermost.com/user/Haliax), [hanzei](https://github.com/hanzei), [harshilsharma63](https://github.com/harshilsharma63), [henrique](https://translate.mattermost.com/user/henrique), [hmhealey](https://github.com/hmhealey), [Honsei901](https://github.com/Honsei901), [hpflatorre](https://github.com/hpflatorre), [ifoukarakis](https://github.com/ifoukarakis), [isacikgoz](https://github.com/isacikgoz), [jespino](https://github.com/jespino), [jessiekahn](https://github.com/jessiekahn), [joakim.rivera](https://translate.mattermost.com/user/joakim.rivera), [johnsonbrothers](https://github.com/johnsonbrothers), [jprusch](https://translate.mattermost.com/user/jprusch), [jwilander](https://github.com/jwilander), [kaakaa](https://github.com/kaakaa), [kayazeren](https://github.com/kayazeren), [Kshitij-Katiyar](https://github.com/Kshitij-Katiyar), [Kuruyia](https://github.com/Kuruyia), [kyrillosisaac2](https://github.com/kyrillosisaac2), [lani009](https://translate.mattermost.com/user/lani009), [larkox](https://github.com/larkox), [lieut-data](https://github.com/lieut-data), [lorumic](https://github.com/lorumic), [lynn915](https://github.com/lynn915), [M-ZubairAhmed](https://github.com/M-ZubairAhmed), [majo](https://translate.mattermost.com/user/majo), [marianunez](https://github.com/marianunez), [massimo](https://translate.mattermost.com/user/massimo), [master7](https://translate.mattermost.com/user/master7), [matt-w99](https://github.com/matt-w99), [matthew-w](https://translate.mattermost.com/user/matthew-w), [mh4ckt3mh4ckt1c4s](https://translate.mattermost.com/user/mh4ckt3mh4ckt1c4s), [minchae.lee](https://translate.mattermost.com/user/minchae.lee), [morgancz](https://translate.mattermost.com/user/morgancz), [Morgansvk](https://github.com/Morgansvk), [muratbayan](https://translate.mattermost.com/user/muratbayan), [mvitale1989](https://github.com/mvitale1989), [nbruneau71250](https://translate.mattermost.com/user/nbruneau71250), [nickmisasi](https://github.com/nickmisasi), [nikolaiz](https://translate.mattermost.com/user/nikolaiz), [Nityanand13](https://github.com/Nityanand13), [pmokeev](https://github.com/pmokeev), [potatogim](https://github.com/potatogim), [pvev](https://github.com/pvev), [raghavaggarwal2308](https://github.com/raghavaggarwal2308), [rahimrahman](https://github.com/rahimrahman), [Rajat-Dabade](https://github.com/Rajat-Dabade), [Reinkard](https://github.com/Reinkard), [renaudk](https://github.com/renaudk), [ricardogalvao](https://translate.mattermost.com/user/ricardogalvao), [RS-labhub](https://github.com/RS-labhub), [Rutam21](https://github.com/Rutam21), [saturninoabril](https://github.com/saturninoabril), [sbishel](https://github.com/sbishel), [Sharuru](https://github.com/Sharuru), [stafot](https://github.com/stafot), [streamer45](https://github.com/streamer45), [sypianski](https://translate.mattermost.com/user/sypianski), [TenGentoppa](https://translate.mattermost.com/user/TenGentoppa), [TheInvincibleRalph](https://github.com/TheInvincibleRalph), [ThrRip](https://github.com/ThrRip), [tnir](https://github.com/tnir), [tokipulan](https://translate.mattermost.com/user/tokipulan), [tomdereub](https://translate.mattermost.com/user/tomdereub), [toninis](https://github.com/toninis), [wetneb](https://github.com/wetneb), [wiggin77](https://github.com/wiggin77), [YahyaHaq](https://github.com/YahyaHaq), [yasserfaraazkhan](https://github.com/yasserfaraazkhan), [yesbhautik](https://github.com/yesbhautik), [zenocode-org](https://translate.mattermost.com/user/zenocode-org)

(release-v10.3-feature-release)=
## Release v10.3 - [Feature Release](https://docs.mattermost.com/about/release-policy.html#release-types)

- **10.3.4, released 2025-02-19**
  - Mattermost v10.3.4 contains low to high severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Boards plugin version [v9.1.1](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.1.1).
  - Pre-packaged Playbooks plugin version [v2.1.1](https://github.com/mattermost/mattermost-plugin-playbooks/releases/tag/v2.1.1).
  - Fixed an issue in Compliance Exports whereby a missing file attachment in S3 could prevent the export run from completing [MM-62527](https://mattermost.atlassian.net/browse/MM-62527).
  - Mattermost v10.3.4 contains the following functional changes:
      - A new configuration setting ``ServiceSettings.EnableWebHubChannelIteration`` was added which allows a user to control the performance of websocket broadcasting. By default, this setting is turned off. If it is turned on, it improves the websocket broadcasting performance at the expense of poor performance when users join/leave a channel. It is not recommended to turn it on unless you have atleast 200,000 concurrent users actively using Mattermost.
- **10.3.3, released 2025-01-22**
  - Mattermost v10.3.3 contains critical severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Boards plugin [v9.0.5](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.0.5).
  - Pre-packaged Channel Export plugin [v1.2.1](https://github.com/mattermost/mattermost-plugin-channel-export/releases/tag/v1.2.1).
  - Fixed a panic during LDAP synchronization [MM-61239](https://mattermost.atlassian.net/browse/MM-61239).
  - Fixed an issue where the bulk export retention job would accidentally delete non-bulk export files and directories [MM-60888](https://mattermost.atlassian.net/browse/MM-60888).
  - Mattermost v10.3.3 contains no database or functional changes.
- **10.3.2, released 2025-01-15**
  - Mattermost v10.3.2 contains low to medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Boards plugin [v9.0.2](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.0.2).
  - Fixed an issue with the webhook attachment button style [MM-62400](https://mattermost.atlassian.net/browse/MM-62400).
  - Mattermost v10.3.2 contains no database or functional changes.
- **10.3.1, released 2024-12-16**
  - Fixed an issue where user statuses weren't synced properly between servers [MM-61438](https://mattermost.atlassian.net/browse/MM-61438).
  - Fixed an accessibility problem in the new search input [MM-61234](https://mattermost.atlassian.net/browse/MM-61234).
  - Mattermost v10.3.1 contains no database or functional changes.
- **10.3.0, released 2024-12-16**
  - Original 10.3.0 release.

### Important Upgrade Notes

 - The Classic Mobile App has been phased out. Please download the new v2 Mobile App from the [Apple App Store](https://apps.apple.com/us/app/mattermost/id1257222717) or [Google Play Store](https://play.google.com/store/apps/details?id=com.mattermost.rn). See more details in the [classic mobile app deprecation](https://forum.mattermost.com/t/classic-mobile-app-deprecation/18703) Mattermost forum post.

### Compatibility

 - Updated minimum Edge and Chrome versions to 130+.

```{Important}
If you upgrade from a release earlier than v10.2, please read the other [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html).
```

### Improvements

See [this walkthrough video](https://mattermost.com/video/mattermost-v10-3-changelog/) on some of the highlights and improvements in our latest release below.

#### User Interface (UI)
 - Pre-packaged Calls plugin [v1.3.0](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.3.0).
 - Downgraded Traditional Chinese language to Beta.
 - Added a feature to schedule a message at a future date (Professional and Enterprise plans).
 - Copilot plugin is now installed and enabled by default.
 - Added an option to test notifications.
 - Added a new search interface.
 - Updated product string for clarity.
 - Removed most places where deprecated translation code is used in the web app.
 - Removed some duplicate CSS from the web app bundle.

#### Administration
 - A 200 response is now returned for HEAD requests to a sub-path rather than responding with a 302. This fixes mobile devices trying to connect to a server hosted on a sub-path.
 - Added the ``fetchMissingUsers`` option to ``PostUtils.messageHtmlToComponent`` for use by plugins.
 - Added support for exporting and importing bot users via mmctl.
 - Added a warning to mmctl for cases where a user specifies a per-page parameter that's larger than the maximum value supported.

#### Performance
 - Added Desktop App performance metrics.

### Bug Fixes
 - Fixed an issue with post drafts being unnecessarily saved when changing channels.
 - Fixed an issue where the Web App would feel slower to load than the Desktop App.
 - Fixed an issue where new messages from new channels wouldn't appear in the sidebar after reconnecting the websocket.
 - Fixed an issue with a link in the Compliance Monitoring page banner in the System Console.
 - Fixed an issue that no longer allowed managing user tokens via the System Console.
 - Fixed a SVG image rendering issue by setting conditional width and height attributes in ``ImagePreview`` and ``SizeAwareImage`` components.
 - Fixed an issue with the web app status not being updated correctly for the current user.

### config.json
New setting options were added to ``config.json``. Below is a list of the additions and their default values on install. The settings can be modified in ``config.json``, or the System Console when available.

#### Changes to all plans:
 - Under ``ServiceSettings `` in ``config.json``:
    - Added ``ScheduledPosts`` to enable the feature to schedule and send message in the future.

### Go Version
 - v10.3 is built with Go ``v1.22.6``.

### Open Source Components
 - Added ``opensearch-project/opensearch-go`` to https://github.com/mattermost/mattermost.

### Known Issues
 - The bottom padding is missing in the edit state of a scheduled messages [MM-61722](https://mattermost.atlassian.net/browse/MM-61722).
 - An incorrect count is displayed in channels for scheduled messages [MM-62197](https://mattermost.atlassian.net/browse/MM-62197).
 - The scheduled post channel indicator sometimes ends up in a bad state [MM-62222](https://mattermost.atlassian.net/browse/MM-62222).
 - Scheduled messages are not removed from queued list when sent while being disconnected [MM-62229](https://mattermost.atlassian.net/browse/MM-62229).
 - Scheduled message date displayed for Direct Message users is sometimes incorrect [MM-62244](https://mattermost.atlassian.net/browse/MM-62244).
 - The new search modal doesn't autocomplete after a space [MM-62199](https://mattermost.atlassian.net/browse/MM-62199).
 - Searching stop words in quotation marks with Elasticsearch enabled returns more than just the searched terms.
 - Slack import through the CLI fails if email notifications are enabled.
 - The Playbooks left-hand sidebar doesn't update when a user is added to a run or playbook without a refresh.
 - If a user isn't a member of a configured broadcast channel, posting a status update might fail without any error feedback. As a temporary workaround, join the configured broadcast channels, or remove those channels from the run configuration.

### Contributors
 - [7+7](https://translate.mattermost.com/user/7+7), [abdellani](https://github.com/abdellani), [agarciamontoro](https://github.com/agarciamontoro), [agnivade](https://github.com/agnivade), [akbarkz](https://translate.mattermost.com/user/akbarkz), [Alenoda](https://github.com/Alenoda), [amyblais](https://github.com/amyblais), [amynicol1985](https://github.com/amynicol1985), [and-ri](https://translate.mattermost.com/user/and-ri), [andr-sokolov](https://github.com/andr-sokolov), [andreabia](https://github.com/andreabia), [andrleite](https://github.com/andrleite), [angeloskyratzakos](https://github.com/angeloskyratzakos), [Aryakoste](https://github.com/Aryakoste), [asaadmahmood](https://github.com/asaadmahmood), [AulakhHarsh](https://github.com/AulakhHarsh), [ayusht2810](https://github.com/ayusht2810), [azadDsync](https://github.com/azadDsync), [BenCookie95](https://github.com/BenCookie95), [calebroseland](https://github.com/calebroseland), [callmeott](https://github.com/callmeott), [carlosGuimaraesTc](https://github.com/carlosGuimaraesTc), [catalintomai](https://github.com/catalintomai), [cedric.lamalle](https://translate.mattermost.com/user/cedric.lamalle), [creeper-0910](https://translate.mattermost.com/user/creeper-0910), [crspeller](https://github.com/crspeller), [ctlaltdieliet](https://translate.mattermost.com/user/ctlaltdieliet), [cwarnermm](https://github.com/cwarnermm), [cyberm8](https://github.com/cyberm8), [cyrusjc](https://github.com/cyrusjc), [decke](https://github.com/decke), [devinbinnie](https://github.com/devinbinnie), [Dishika18](https://github.com/Dishika18), [Dzenan](https://translate.mattermost.com/user/Dzenan), [edlerd](https://github.com/edlerd), [Eleferen](https://translate.mattermost.com/user/Eleferen), [enahum](https://github.com/enahum), [esarafianou](https://github.com/esarafianou), [frankps](https://translate.mattermost.com/user/frankps), [fsilye](https://github.com/fsilye), [gabsfrancis](https://translate.mattermost.com/user/gabsfrancis), [Gesare5](https://github.com/Gesare5), [guruprasath-v](https://github.com/guruprasath-v), [hanzei](https://github.com/hanzei), [harshilsharma63](https://github.com/harshilsharma63), [HarshitVashisht11](https://github.com/HarshitVashisht11), [henrique](https://translate.mattermost.com/user/henrique), [hmhealey](https://github.com/hmhealey), [Honsei901](https://github.com/Honsei901), [hpflatorre](https://github.com/hpflatorre), [hun-a](https://github.com/hun-a), [ifoukarakis](https://github.com/ifoukarakis), [isacikgoz](https://github.com/isacikgoz), [Jelmerovereem](https://github.com/Jelmerovereem), [jespino](https://github.com/jespino), [jlandells](https://github.com/jlandells), [johnsonbrothers](https://github.com/johnsonbrothers), [jonathan-dove](https://github.com/jonathan-dove), [jprusch](https://github.com/jprusch), [JulienTant](https://github.com/JulienTant), [jwilander](https://github.com/jwilander), [kaakaa](https://github.com/kaakaa), [kayazeren](https://github.com/kayazeren), [kczpl](https://github.com/kczpl), [Killer2OP](https://github.com/Killer2OP), [Kshitij-Katiyar](https://github.com/Kshitij-Katiyar), [Kuruyia](https://github.com/Kuruyia), [KuSh](https://github.com/KuSh), [kyrillosisaac2](https://github.com/kyrillosisaac2), [larkox](https://github.com/larkox), [lieut-data](https://github.com/lieut-data), [lynn915](https://github.com/lynn915), [M-ZubairAhmed](https://github.com/M-ZubairAhmed), [majo](https://translate.mattermost.com/user/majo), [mas-who](https://github.com/mas-who), [master7](https://translate.mattermost.com/user/master7), [matt-w99](https://github.com/matt-w99), [matthew-w](https://translate.mattermost.com/user/matthew-w), [matthewbirtch](https://github.com/matthewbirtch), [mentz](https://translate.mattermost.com/user/mentz), [minkyngkm](https://github.com/minkyngkm), [molejnik88](https://github.com/molejnik88), [morgancz](https://translate.mattermost.com/user/morgancz), [Morgansvk](https://github.com/Morgansvk), [mvitale1989](https://github.com/mvitale1989), [NadavTasher](https://github.com/NadavTasher), [nickmisasi](https://github.com/nickmisasi), [Niharika0104](https://github.com/Niharika0104), [nikolaiz](https://translate.mattermost.com/user/nikolaiz), [NilsArnlund](https://github.com/NilsArnlund), [potatogim](https://translate.mattermost.com/user/potatogim), [pranay-0512](https://github.com/pranay-0512), [pvev](https://github.com/pvev), [raghavaggarwal2308](https://github.com/raghavaggarwal2308), [rahimrahman](https://github.com/rahimrahman), [Rajat-Dabade](https://github.com/Rajat-Dabade), [Reinkard](https://github.com/Reinkard), [ricardogalvao](https://translate.mattermost.com/user/ricardogalvao), [RS-labhub](https://github.com/RS-labhub), [Rutam21](https://github.com/Rutam21), [s1Sharp](https://github.com/s1Sharp), [samarth29jc](https://github.com/samarth29jc), [saturninoabril](https://github.com/saturninoabril), [sbishel](https://github.com/sbishel), [Seyifunmi](https://github.com/Seyifunmi), [Sharuru](https://github.com/Sharuru), [sohzm](https://github.com/sohzm), [sparr](https://github.com/sparr), [srisri332](https://github.com/srisri332), [stafot](https://github.com/stafot), [streamer45](https://github.com/streamer45), [stylianosrigas](https://github.com/stylianosrigas), [sumedhakoranga](https://github.com/sumedhakoranga), [TheInvincibleRalph](https://github.com/TheInvincibleRalph), [thelizardreborn](https://github.com/thelizardreborn), [theoforger](https://github.com/theoforger), [ThrRip](https://translate.mattermost.com/user/ThrRip), [tokipulan](https://translate.mattermost.com/user/tokipulan), [toninis](https://github.com/toninis), [verdel](https://github.com/verdel), [Victor-Nyagudi](https://github.com/Victor-Nyagudi), [vish9812](https://github.com/vish9812), [wetneb](https://github.com/wetneb), [wiggin77](https://github.com/wiggin77), [Willyfrog](https://github.com/Willyfrog), [willypuzzle](https://github.com/willypuzzle), [yanyiyi](https://github.com/yanyiyi), [yasserfaraazkhan](https://github.com/yasserfaraazkhan), [yesbhautik](https://github.com/yesbhautik)

(release-v10.2-feature-release)=
## Release v10.2 - [Feature Release](https://docs.mattermost.com/about/release-policy.html#release-types)

- **10.2.3, released 2025-01-22**
  - Mattermost v10.2.3 contains critical severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Boards plugin [v9.0.5](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.0.5).
  - Pre-packaged Channel Export plugin [v1.2.1](https://github.com/mattermost/mattermost-plugin-channel-export/releases/tag/v1.2.1).
  - Fixed a panic during LDAP synchronization [MM-61239](https://mattermost.atlassian.net/browse/MM-61239).
  - Fixed an issue where the bulk export retention job would accidentally delete non-bulk export files and directories [MM-60888](https://mattermost.atlassian.net/browse/MM-60888).
  - Mattermost v10.2.3 contains no database or functional changes.
- **10.2.2, released 2025-01-15**
  - Mattermost v10.2.2 contains low to medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Boards plugin [v9.0.2](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.0.2).
  - Mattermost v10.2.2 contains no database or functional changes.
- **10.2.1, released 2024-12-10**
  - Mattermost v10.2.1 contains low to medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Fixed an issue where plugin settings got wiped if the plugin declared some of its fields as secrets [MM-61441](https://mattermost.atlassian.net/browse/MM-61441).
  - Pre-packaged Calls plugin [v1.3.2](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.3.2).
  - Mattermost v10.2.1 contains no database or functional changes.
- **10.2.0, released 2024-11-15**
  - Original 10.2.0 release.

### Important Upgrade Notes

 - Docker Content Trust (DCT) for signing Docker image artifacts has been replaced by Sigstore Cosign in v10.2 (November, 2024). If you rely on artifact verification using DCT, please [transition to using Cosign](https://edu.chainguard.dev/open-source/sigstore/cosign/how-to-install-cosign/). See the [DCT deprecation Mattermost forum post](https://forum.mattermost.com/t/upcoming-dct-deprecation/19275) for more details. 

```{Important}
If you upgrade from a release earlier than v10.0, please read the other [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html).
```

### Improvements

See [this walkthrough video](https://mattermost.com/video/mattermost-v10-2-changelog/) on some of the highlights and improvements in our latest release below.

#### User Interface (UI)
 - Pre-packaged Calls plugin [v1.2.1](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.2.1).
 - Changed the logic of ``useMilitaryTime`` to ``false`` to default to 12-hour time format unless the user's preference from ``data.Value`` is ``true``. When a notification email is sent to a user, the time should now default to the 12-hour format unless otherwise stated by the user. 
 - A warning is now shown when deleting a post or comment from a remote/shared channel.
 - Bot messages will now properly mention both users when they happen on non-bot Direct Messages.
 - Updated the channel header to hide pinned posts when there aren't any in the channel.
 - Added full support for @mentions in the values of fields in message attachments.

#### Administration
 - Added a new URL parameter called ``permanent`` to ``DELETE /api/v4/posts/<post-id>``, and set ``permanent`` to ``true`` in order to permanently delete a post and its attachments.
 - Added Connected Workspaces (Beta) administration page to the System Console when Connected Workspaces are [enabled](https://docs.mattermost.com/onboard/connected-workspaces.html#enable-connected-workflows) for the server.
 - Added a team selector to accept connection invite flow in Connected Workspaces.
 - Restricted activation and deactivation of LDAP-managed users through both the System Console UI and Mattermost API.
 - Export/import improvements: added the ability to export all user preferences and flagged posts.
 - Increased timeouts to fetch cluster logs.
 - Improved log messages for cluster communication.
 - Information about deleted rows from the Data Retention job are now logged.
 - License details to logs are now emitted when added or removed.
 - Added a new mmctl command, ``mmctl post delete <post-id>``, in order to permanently delete a post and its attachments.

#### Performance
 - Added metrics to prometheus to check the mobile versions for each session daily.
 - Improved the performance of LDAP sync jobs when group-contained teams and channels are used.
 - Added minor improvements to notification metrics.
 - Added minor improvements to mobile push notifications.

### Bug Fixes
 - Fixed an issue with email notifications using 24-hour timestamps by default.
 - Fixed an issue where bots were not ignored when counting deactivated accounts for statistics.
 - Fixed an issue where drafts didn’t allow scrolling if the user had many drafts.
 - Fixed an issue that caused Javascript errors in the System Console.
 - Fixed racy use of session in ``NewWebConn``.
 - Fixed a race condition that would happen after a server start if ``EnableTesting`` was enabled.
 - Fixed an issue where no error message was shown when replying to a deleted post from the draft screen.
 - Fixed an issue where the check icons were missing from the Sort and Show options in the Direct Messages tab, and the Sort tab of the Channels tab.
 - Fixed desyncing issues with unreads between the team sidebar and the title bar.
 - Fixed an issue with message export file attachments with dedicated filestore: when the dedicated filestore is set, file attachments will be found and exported correctly.
 - Reverted a change enforcing usernames to start with alpha characters on the server.
 - Reverted a breaking change in ``registerSlashCommandWillBePostedHook`` that caused errors to surface in case an expected empty object was returned.

### config.json
New setting options were added to ``config.json``. Below is a list of the additions and their default values on install. The settings can be modified in ``config.json``, or the System Console when available.

#### Changes to all plans:
 - Under ``ServiceSettings`` in ``config.json``:
    - Added a new configuration setting ``EnableAPIPostDeletion`` in order to enable/disable post deletion. This configuration setting does not need to be enabled when running mmctl in local mode.
    - Added ``EnableDesktopLandingPage`` to allow the desktop app landing page to be disabled.
 - Under ``NativeAppSettings`` in ``config.json``:
     - Added a configuration setting ``MobileExternalBrowser`` that tells the Mobile app to perform SSO Authentication using the external default browser.

### Go Version
 - v10.2 is built with Go ``v1.22.6``.

### Known Issues
 - The scrollbar is not clickable when there is a "Jump to recents" toaster [MM-61526](https://mattermost.atlassian.net/browse/MM-61526).
 - Shared Channels: Direct Messages are not supported.
 - Searching stop words in quotation marks with Elasticsearch enabled returns more than just the searched terms.
 - Slack import through the CLI fails if email notifications are enabled.
 - The Playbooks left-hand sidebar doesn't update when a user is added to a run or playbook without a refresh.
 - If a user isn't a member of a configured broadcast channel, posting a status update might fail without any error feedback. As a temporary workaround, join the configured broadcast channels, or remove those channels from the run configuration.

### Contributors
 - [047pegasus](https://github.com/047pegasus), [1510janu](https://github.com/1510janu), [aamfahim](https://github.com/aamfahim), [aditipatelpro](https://github.com/aditipatelpro), [agarciamontoro](https://github.com/agarciamontoro), [agnivade](https://github.com/agnivade), [amyblais](https://github.com/amyblais), [andreabia](https://translate.mattermost.com/user/andreabia), [andrleite](https://github.com/andrleite), [angeloskyratzakos](https://github.com/angeloskyratzakos), [anudhyan](https://github.com/anudhyan), [Arch130](https://github.com/Arch130), [arilloid](https://github.com/arilloid), [Aryakoste](https://github.com/Aryakoste), [asaadmahmood](https://github.com/asaadmahmood), [azadDsync](https://github.com/azadDsync), [azigler](https://github.com/azigler), [belkhoujaons](https://github.com/belkhoujaons), [BenCookie95](https://github.com/BenCookie95), [calebroseland](https://github.com/calebroseland), [Camillarhi](https://github.com/Camillarhi), [CarlssonFilip](https://github.com/CarlssonFilip), [catalintomai](https://github.com/catalintomai), [CBID2](https://github.com/CBID2), [cpoile](https://github.com/cpoile), [crspeller](https://github.com/crspeller), [ctlaltdieliet](https://github.com/ctlaltdieliet), [cwarnermm](https://github.com/cwarnermm), [danielsischy](https://github.com/danielsischy), [devinbinnie](https://github.com/devinbinnie), [DHaussermann](https://github.com/DHaussermann), [diamant3](https://github.com/diamant3), [Dishika18](https://github.com/Dishika18), [Eleferen](https://translate.mattermost.com/user/Eleferen), [emdecr](https://github.com/emdecr), [enahum](https://github.com/enahum), [enzowritescode](https://github.com/enzowritescode), [esarafianou](https://github.com/esarafianou), [esethna](https://github.com/esethna), [fmartingr](https://github.com/fmartingr), [frankps](https://translate.mattermost.com/user/frankps), [fsilye](https://github.com/fsilye), [fume4mattermost](https://github.com/fume4mattermost), [gabrieljackson](https://github.com/gabrieljackson), [Gesare5](https://github.com/Gesare5), [Good-Soma](https://github.com/Good-Soma), [grubbins](https://github.com/grubbins), [gvarma28](https://github.com/gvarma28), [hamzawritescode](https://github.com/hamzawritescode), [hannaparks](https://github.com/hannaparks), [hanzei](https://github.com/hanzei), [HarshitVashisht11](https://github.com/HarshitVashisht11), [hereje](https://github.com/hereje), [hmhealey](https://github.com/hmhealey), [ifoukarakis](https://github.com/ifoukarakis), [isacikgoz](https://github.com/isacikgoz), [ja49619](https://translate.mattermost.com/user/ja49619), [jespino](https://github.com/jespino), [jlandells](https://github.com/jlandells), [johnsonbrothers](https://github.com/johnsonbrothers), [jopaleti](https://github.com/jopaleti), [jprusch](https://github.com/jprusch), [jwilander](https://github.com/jwilander), [kaakaa](https://github.com/kaakaa), [kayazeren](https://github.com/kayazeren), [Killer2OP](https://github.com/Killer2OP), [kom-senapati](https://github.com/kom-senapati), [Kshitij-Katiyar](https://github.com/Kshitij-Katiyar), [KuSh](https://github.com/KuSh), [KvngMikey](https://github.com/KvngMikey), [larkox](https://github.com/larkox), [lieut-data](https://github.com/lieut-data), [lynn915](https://github.com/lynn915), [M-ZubairAhmed](https://github.com/M-ZubairAhmed), [majo](https://translate.mattermost.com/user/majo), [Malay-dev](https://github.com/Malay-dev), [master7](https://translate.mattermost.com/user/master7), [matthew-w](https://translate.mattermost.com/user/matthew-w), [matthewbirtch](https://github.com/matthewbirtch), [mgdelacroix](https://github.com/mgdelacroix), [mm-prodsec-bot](https://github.com/mm-prodsec-bot), [moda-l10n](https://translate.mattermost.com/user/moda-l10n), [Morgan_svk](https://translate.mattermost.com/user/Morgan_svk), [Movion](https://github.com/Movion), [mvitale1989](https://github.com/mvitale1989), [nickmisasi](https://github.com/nickmisasi), [Niharika0104](https://github.com/Niharika0104), [nikolaiz](https://translate.mattermost.com/user/nikolaiz), [NilsArnlund](https://github.com/NilsArnlund), [panoramix360](https://github.com/panoramix360), [pradeepmurugesan](https://github.com/pradeepmurugesan), [pvev](https://github.com/pvev), [qfrigolac](https://github.com/qfrigolac), [raghavaggarwal2308](https://github.com/raghavaggarwal2308), [rahimrahman](https://github.com/rahimrahman), [Rajat-Dabade](https://github.com/Rajat-Dabade), [Ranjana761](https://github.com/Ranjana761), [raremax](https://translate.mattermost.com/user/raremax), [Reinkard](https://github.com/Reinkard), [RS-labhub](https://github.com/RS-labhub), [Ruhi14](https://github.com/Ruhi14), [Rutam21](https://github.com/Rutam21), [s4kh](https://github.com/s4kh), [sahariardev](https://github.com/sahariardev), [samarth29jc](https://github.com/samarth29jc), [saturninoabril](https://github.com/saturninoabril), [sbishel](https://github.com/sbishel), [sedivst](https://translate.mattermost.com/user/sedivst), [Sharuru](https://translate.mattermost.com/user/Sharuru), [shraddha761](https://github.com/shraddha761), [space-w-alker](https://github.com/space-w-alker), [srisri332](https://github.com/srisri332), [stafot](https://github.com/stafot), [streamer45](https://github.com/streamer45), [stylianosrigas](https://github.com/stylianosrigas), [svelle](https://github.com/svelle), [swills](https://github.com/swills), [tanmaythole](https://github.com/tanmaythole), [TealWater](https://github.com/TealWater), [TheInvincibleRalph](https://github.com/TheInvincibleRalph), [theoforger](https://github.com/theoforger), [ThrRip](https://github.com/ThrRip), [TomerPacific](https://github.com/TomerPacific), [toninis](https://github.com/toninis), [varghesejose2020](https://github.com/varghesejose2020), [vawaver](https://translate.mattermost.com/user/vawaver), [vhaska](https://translate.mattermost.com/user/vhaska), [Victor-Nyagudi](https://github.com/Victor-Nyagudi), [vish9812](https://github.com/vish9812), [WeBjAnJaN](https://translate.mattermost.com/user/WeBjAnJaN), [wetneb](https://github.com/wetneb), [wiggin77](https://github.com/wiggin77), [Willyfrog](https://github.com/Willyfrog), [yanyiyi](https://github.com/yanyiyi), [yasserfaraazkhan](https://github.com/yasserfaraazkhan), [z44440000z](https://github.com/z44440000z), [ZubairImtiaz3](https://github.com/ZubairImtiaz3)

(release-v10.1-feature-release)=
## Release v10.1 - [Feature Release](https://docs.mattermost.com/about/release-policy.html#release-types)

- **10.1.7, released 2025-01-15**
  - Mattermost v10.1.7 contains low to medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Boards plugin [v9.0.2](https://github.com/mattermost/mattermost-plugin-boards/releases/tag/v9.0.2).
  - Mattermost v10.1.7 contains no database or functional changes.
- **10.1.6, released 2024-12-20**
  - Fixed an issue by restoring System Administrator access to Direct and Group Messages without being a member.
  - Mattermost v10.1.6 contains no database or functional changes.
- **10.1.5, released 2024-12-18**
  - Fixed an issue where System Administrators could not pull posts in from Direct Message channels they were not in [MM-62092](https://mattermost.atlassian.net/browse/MM-62092).
  - Mattermost v10.1.5 contains no database or functional changes.
- **10.1.4, released 2024-12-10**
  - Mattermost v10.1.4 contains low to medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Calls plugin [v1.3.2](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.3.2).
  - Mattermost v10.1.4 contains no database or functional changes.
- **10.1.3, released 2024-11-14**
  - Mattermost v10.1.3 contains medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Reverted a change enforcing usernames to start with alpha characters on the server [MM-61143](https://mattermost.atlassian.net/browse/MM-61143).
  - Reverted a breaking change in ``registerSlashCommandWillBePostedHook`` that caused errors to surface in case an expected empty object was returned [MM-61233](https://mattermost.atlassian.net/browse/MM-61233).
  - Mattermost v10.1.3 contains no database or functional changes.
- **10.1.2, released 2024-10-28**
  - Mattermost v10.1.2 contains a high severity level security fix. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Fixed an issue with message export file attachments with a dedicated filestore [MM-60063](https://mattermost.atlassian.net/browse/MM-60063).
  - Mattermost v10.1.2 contains the following functional change:
      - Added a configuration setting **NativeAppSettings > MobileExternalBrowser** that tells the Mobile app to perform SSO Authentication using the external default browser [MM-60332](https://mattermost.atlassian.net/browse/MM-60332).
- **10.1.1, released 2024-10-16**
  - Fixed an issue where a shared indicator was shown in all Direct Messages, regardless of the user coming from a shared server [MM-60744](https://mattermost.atlassian.net/browse/MM-60744).
  - Mattermost v10.1.1 contains no database or functional changes.
- **10.1.0, released 2024-10-16**
  - Original 10.1.0 release.

```{Important}
If you upgrade from a release earlier than v10.0, please read the other [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html).
```

### Improvements

#### User Interface (UI)
 - Added Metrics plugin to the prepackaged plugins, [v0.5.3](https://github.com/mattermost/mattermost-plugin-metrics/releases/tag/v0.5.3).
 - Pre-packaged Calls plugin [v1.1.0](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.1.0).
 - Enabled Channel Bookmarks, added re-ordering, and fixed URL validity checking.
 - Added a more descriptive error message, "Uploaded plugin size exceeds limit." for plugin uploads that are too large.
 - Added channel specific message notification sounds configuration.

#### Administration
 - Added ``DeleteAt`` field for ``SharedChannelRemotes`` and ``RemoteClusters``.
 - Added support for sending channel invites to offline remotes in Shared Channels.
 - Changed server-side logic to return a ``413: Request Entity Too Large`` HTTP status code for a plugin upload that is too large.
 - Direct and Group Message unread/read state over export and import will now be carried over.
 - CRT memberships are now importable for import.
 - CRT memberships are now exportable for bulk export.
 - Added ``--local mode`` support in MMCTL to handle user preferences.
 - Plugins are now allowed to mark setting fields as secret, obfuscating them in the System Console and the Support Packet.

#### Performance
 - Improved metrics related to push proxy errors.
 - Improved metrics around notifications.

### Bug Fixes
 - Fixed an issue where threads would be marked as read if they were open in the background.
 - Fixed an issue where Direct and Group Messages didn't load correctly in the sidebar when refreshing the app from Drafts.
 - Fixed an issue attempting to bind to Apps plugin when the plugin was not enabled.
 - Fixed an issue where the Unreads tab would not update correctly after the websocket reconnected.
 - Fixed an issue with focusing on the main box when loading the app.
 - Fixed an issue where Team and Channel Admins could lose the ability to create posts in a moderated channel.
 - Fixed an issue where marking a channel as unread did not show immediately in other clients.
 - Fixed an issue with not allowing to use ``@`` and ``~`` in the ``in:`` search modifier without affecting search results.
 - Fixed an issue with YouTube previews no longer being displayed.

### config.json
New setting options were added to ``config.json``. Below is a list of the additions and their default values on install. The settings can be modified in ``config.json``, or the System Console when available.

#### Changes to all plans:
 - Under ``ExperimentalSettings`` in ``config.json``:
    - Added ``YoutubeReferrerPolicy`` to fix an issue where YouTube previews showed an “Video Unavailable” error instead of the video.

#### Changes to the Enterprise plan:
 - Under ``ConnectedWorkspacesSettings`` in ``config.json``:
    - Added ``DisableSharedChannelsStatusSync`` to add status sync support to Shared Channels.
 - Under ``ConnectedWorkspacesSettings`` in ``config.json``:
    - Moved the Shared Channel related configuration properties out of the Experimental section.
    - Added the ``MaxPostsPerSync`` configuration property.

### API Changes
 - Added new API endpoints to manage shared channels.
 - Added proper response to ``/api/v4/client_perf`` endpoint.

### Go Version
 - v10.1 is built with Go ``v1.22.6``.

### Known Issues
 - Searching stop words in quotation marks with Elasticsearch enabled returns more than just the searched terms.
 - Slack import through the CLI fails if email notifications are enabled.
 - The Playbooks left-hand sidebar doesn't update when a user is added to a run or playbook without a refresh.
 - If a user isn't a member of a configured broadcast channel, posting a status update might fail without any error feedback. As a temporary workaround, join the configured broadcast channels, or remove those channels from the run configuration.

### Contributors
 - [adityasoni2019](https://github.com/adityasoni2019), [agarciamontoro](https://github.com/agarciamontoro), [agnivade](https://github.com/agnivade), [algeorgiadis](https://github.com/algeorgiadis), [amyblais](https://github.com/amyblais), [andreabia](https://translate.mattermost.com/user/andreabia), [andrleite](https://github.com/andrleite), [angeloskyratzakos](https://github.com/angeloskyratzakos), [armmanvaillancourt](https://github.com/armmanvaillancourt), [Aryakoste](https://github.com/Aryakoste), [ayusht2810](https://github.com/ayusht2810), [azistellar](https://translate.mattermost.com/user/azistellar), [azizthegit](https://github.com/azizthegit), [BenCookie95](https://github.com/BenCookie95), [calebroseland](https://github.com/calebroseland), [catalintomai](https://github.com/catalintomai), [ChinoUkaegbu](https://github.com/ChinoUkaegbu), [Chlbek](https://translate.mattermost.com/user/Chlbek), [crspeller](https://github.com/crspeller), [ctlaltdieliet](https://translate.mattermost.com/user/ctlaltdieliet), [cwarnermm](https://github.com/cwarnermm), [danielsischy](https://github.com/danielsischy), [daveseo901](https://github.com/daveseo901), [devinbinnie](https://github.com/devinbinnie), [DHaussermann](https://github.com/DHaussermann), [Eleferen](https://translate.mattermost.com/user/Eleferen), [emdecr](https://github.com/emdecr), [enahum](https://github.com/enahum), [enzowritescode](https://github.com/enzowritescode), [esarafianou](https://github.com/esarafianou), [esethna](https://github.com/esethna), [fmartingr](https://github.com/fmartingr), [frankps](https://translate.mattermost.com/user/frankps), [fsilye](https://github.com/fsilye), [gabrieljackson](https://github.com/gabrieljackson), [Gesare5](https://github.com/Gesare5), [Glandos](https://github.com/Glandos), [grundleborg](https://github.com/grundleborg), [gvarma28](https://github.com/gvarma28), [hanzei](https://github.com/hanzei), [harshilsharma63](https://github.com/harshilsharma63), [hereje](https://github.com/hereje), [hmhealey](https://github.com/hmhealey), [ifoukarakis](https://github.com/ifoukarakis), [isacikgoz](https://github.com/isacikgoz), [ja49619](https://translate.mattermost.com/user/ja49619), [johnsonbrothers](https://github.com/johnsonbrothers), [jones](https://translate.mattermost.com/user/jones), [jprusch](https://github.com/jprusch), [JulienTant](https://github.com/JulienTant), [jwilander](https://github.com/jwilander), [kaakaa](https://github.com/kaakaa), [kaoski](https://github.com/kaoski), [kayazeren](https://github.com/kayazeren), [Kshitij-Katiyar](https://github.com/Kshitij-Katiyar), [L3o-pold](https://github.com/L3o-pold), [larkox](https://github.com/larkox), [lieut-data](https://github.com/lieut-data), [lindalumitchell](https://github.com/lindalumitchell), [lukasMega](https://github.com/lukasMega), [M-ZubairAhmed](https://github.com/M-ZubairAhmed), [majo](https://translate.mattermost.com/user/majo), [manujgrover71](https://github.com/manujgrover71), [master7](https://translate.mattermost.com/user/master7), [matt-w99](https://github.com/matt-w99), [matthew-w](https://translate.mattermost.com/user/matthew-w), [matthewbirtch](https://github.com/matthewbirtch), [mgdelacroix](https://github.com/mgdelacroix), [milotype](https://translate.mattermost.com/user/milotype), [Morgan_svk](https://translate.mattermost.com/user/Morgan_svk), [Movion](https://github.com/Movion), [mvitale1989](https://github.com/mvitale1989), [nekodayo2222](https://translate.mattermost.com/user/nekodayo2222), [nickmisasi](https://github.com/nickmisasi), [nikhilskul7](https://github.com/nikhilskul7), [Porma120](https://github.com/Porma120), [pvev](https://github.com/pvev), [raghavaggarwal2308](https://github.com/raghavaggarwal2308), [rahimrahman](https://github.com/rahimrahman), [Rajat-Dabade](https://github.com/Rajat-Dabade), [Rishiii7](https://github.com/Rishiii7), [saturninoabril](https://github.com/saturninoabril), [sbishel](https://github.com/sbishel), [Sharuru](https://github.com/Sharuru), [stafot](https://github.com/stafot), [streamer45](https://github.com/streamer45), [stylianosrigas](https://github.com/stylianosrigas), [testtomato1230](https://translate.mattermost.com/user/testtomato1230), [TheInvincibleRalph](https://github.com/TheInvincibleRalph), [ThrRip](https://translate.mattermost.com/user/ThrRip), [toninis](https://github.com/toninis), [tsabi](https://github.com/tsabi), [vish9812](https://github.com/vish9812), [wiggin77](https://github.com/wiggin77), [Willyfrog](https://github.com/Willyfrog), [yasserfaraazkhan](https://github.com/yasserfaraazkhan), [yaz](https://translate.mattermost.com/user/yaz), [yuney-worx4you](https://github.com/yuney-worx4you)

(release-v10.0-major-release)=
## Release v10.0 - [Major Release](https://docs.mattermost.com/about/release-policy.html#release-types)

- **10.0.4, released 2024-12-10**
  - Mattermost v10.0.4 contains low to medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Pre-packaged Calls plugin [v1.3.2](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.3.2).
  - Mattermost v10.0.4 contains no database or functional changes.
- **10.0.3, released 2024-11-14**
  - Mattermost v10.0.3 contains medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Mattermost v10.0.3 contains no database or functional changes.
- **10.0.2, released 2024-10-28**
  - Mattermost v10.0.2 contains a high severity level security fix. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Reverted a change enforcing usernames to start with alpha characters on the server [MM-61143](https://mattermost.atlassian.net/browse/MM-61143).
  - Reverted a breaking change in ``registerSlashCommandWillBePostedHook`` that caused errors to surface in case an expected empty object was returned [MM-61233](https://mattermost.atlassian.net/browse/MM-61233).
  - Mattermost v10.0.2 contains no database or functional changes.
- **10.0.1, released 2024-10-10**
  - Mattermost v10.0.1 contains low to medium severity level security fixes. [Upgrading](https://docs.mattermost.com/upgrade/upgrading-mattermost-server.html) to this release is recommended. Details will be posted on our [security updates page](https://mattermost.com/security-updates/) 30 days after release as per the [Mattermost Responsible Disclosure Policy](https://mattermost.com/security-vulnerability-report/).
  - Fixed an issue enabling Professional customers and Team Edition users to upgrade to Playbooks v2 via the in-product marketplace, which fails to start without an Enterprise License. Additional details and discussion can be found on the [forums here](https://forum.mattermost.com/t/clarification-on-playbooks-in-mattermost-v10/20563) [MM-60679](https://mattermost.atlassian.net/browse/MM-60679).
  - Mattermost v10.0.1 contains no database or functional changes.
- **10.0.0, released 2024-09-16**
  - Original 10.0.0 release.

### Important Upgrade Notes
 - We no longer support new installations using MySQL starting in v10. All new customers and/or deployments will only be supported with the minimum supported version of the PostgreSQL database. End of support for MySQL is targeted for Mattermost v11.
 - Apps Framework is deprecated for new installs. Please extend Mattermost using webhooks, slash commands, OAuth2 apps, and plugins.
 - Mattermost v10 introduces Playbooks v2 for all Enterprise licensed customers. Professional SKU customers may continue to use Playbooks v1 uninterrupted which will be maintained and supported until September 2025, followed by an appropriate grandfathering strategy. More detailed information and the discussion are available on the [Mattermost discussion forum](https://forum.mattermost.com/t/clarification-on-playbooks-in-mattermost-v10/20563).
 - Renamed ``Channel Moderation`` to ``Advanced Access Control`` in the channel management section in the **System Console**.
 - Renamed announcement banner feature to “system-wide notifications”.
 - Renamed “Collapsed Reply Threads” to “Threaded Discussions” in the System Console.
 - Renamed “System Roles” to “Delegated Granular Administration” in the System Console.
 - Renamed "Office 365" to "Entra ID" for SSO logins.
 - Fully deprecated the ``/api/v4/image`` endpoint when the image proxy is disabled.
 - Pre-packaged Calls plugin [v1.0.1](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.0.1). This includes breaking changes including removal of group calls from unlicensed servers in order to focus supportability and quality on licensed servers. Unlicensed servers can continue to use Calls in direct message channels, which represent the majority of activity.
 - Removed deprecated ``Config.ProductSettings``, ``LdapSettings.Trace``, and ``AdvancedLoggingConfig`` configuration fields.
 - Removed deprecated ``pageSize`` query parameter from most API endpoints.
 - Deprecated the experimental Strict CSRF token enforcement. This feature will be fully removed in Mattermost v11.

```{Important}
If you upgrade from a release earlier than v9.11, please read the other [Important Upgrade Notes](https://docs.mattermost.com/upgrade/important-upgrade-notes.html).
```

### Highlights

See [this walkthrough video](https://mattermost.com/video/mattermost-v10-0-changelog/) on some of the highlights and improvements in our latest release below.

#### Mattermost Microsoft Teams Plugin
 - Pre-packaged the Microsoft Teams plugin for Mattermost, [v2.0.3](https://github.com/mattermost/mattermost-plugin-msteams/releases/tag/v2.0.3).

#### Mattermost Microsoft Calendar and Microsoft Teams Meetings Plugins
 - Pre-packaged Microsoft Calendar Integration [v1.3.4](https://github.com/mattermost/mattermost-plugin-mscalendar/releases/tag/v1.3.4) and Microsoft Teams Meetings [v2.2.0](https://github.com/mattermost-community/mattermost-plugin-msteams-meetings/releases/tag/v2.2.0) plugins.

#### Mattermost Copilot GA
 - Pre-packaged Mattermost Copilot plugin version [v1.0.0](https://github.com/mattermost/mattermost-plugin-ai/releases/tag/v1.0.0).

### Improvements

#### User Interface (UI)
 - Pre-packaged Calls plugin [v1.0.1](https://github.com/mattermost/mattermost-plugin-calls/releases/tag/v1.0.1).
 - Added Playbooks [v2.0.1](https://github.com/mattermost/mattermost-plugin-playbooks/releases/tag/v2.0.1) to the prepackaged plugins.
 - Added Mattermost user survey plugin to pre-packaged plugins, [v1.1.1](https://github.com/mattermost/mattermost-plugin-user-survey/releases).
 - Changed the right-hand side scroll direction and fixed the advanced text editor to the bottom.
 - Added Do not disturb and late timezone warnings to Direct Message posts.
 - Added user statuses to the Group Members modal.
 - Added labels for channel header and purpose in the right-hand side channel info view.
 - Added pagination user interface to the ``BackstageList`` component.
 - Made various improvements to code involving user preferences.
 - Promoted GIF picker, custom groups and message priority out of Beta.
 - Removed the **Pre-release features** section from **Settings > Advanced** due to lack of usage.

#### Administration
 - Made payload size limit error more clearly visible and recognisable in API responses and server error logs.
 - Extended the plugin schema to support defining sections for **System Console** settings.
 - Added support for a default team on secure connections for incoming channel invites.
 - Remote clusters can now be created without explicitly providing a password.
 - Files are now fetched from all nodes in a cluster when generating a Support Packet.
 - Docker images are now based on Ubuntu Noble.

#### Performance
 - Removed a re-render on channel change.
 - Batched requests made by certain components for loading users and their statuses from the server.
 - Cleaned up some unused post handling logic.

### Bug Fixes
 - Fixed an issue with web app notifications not being shown in the **Notification Center** on Windows or Mac.
 - Fixed an issue with ``mmctl webhooks list`` to paginate past 200 results.
 - Fixed an issue where scrolling capability and a visible scrollbar were missing in post textboxes.
 - Fixed an issue where false warnings about Channel indexes being incorrect were sent to system admins.
 - Fixed an issue where indexing would always be done async even after setting ``LiveIndexingBatchSize`` to ``1``. Now we respect the config and index synchronously if the value is set to ``1``.
 - Fixed an issue where the **Edit Post Time Limit** button was not being displayed in the System Console.
 - Fixed another issue where users would not see channels they were added to/messages from those channels in clustered environments.

### config.json
New setting options were added to ``config.json``. Below is a list of the additions and their default values on install. The settings can be modified in ``config.json``, or the System Console when available.

#### Changes to all plans:
 - Under ``ServiceSettings`` in ``config.json``:
    - Added a new setting ``MaximumURLLength`` to remove the hardcoded URL length limit.
 - Removed deprecated ``Config.ProductSettings``.
 - Removed ``EnablePreviewFeatures`` setting.

#### Changes to the Enterprise plan:
 - Removed deprecated ``LdapSettings.Trace`` setting.
 - Removed deprecated ``AdvancedLoggingConfig`` setting.

### API Changes
 - Reduced the number of API requests made to fetch user information for Group Messages on page load.
 - User APIs now enforce username beginning with alphabetic character, matching client-side validation.
 - Added a new request parameter ``include_total_count`` to API endpoint ``GET /api/v4/hooks/incoming``.

### Go Version
 - v10.0 is built with Go ``v1.21.8``.

### Open Source Components
 - Added ``redis/rueidis`` to https://github.com/mattermost/mattermost.

### Known Issues
 - The cursor is not placed in the "Write to" field on login [MM-60275](https://mattermost.atlassian.net/browse/MM-60275).
 - Searching stop words in quotation marks with Elasticsearch enabled returns more than just the searched terms.
 - Slack import through the CLI fails if email notifications are enabled.
 - The Playbooks left-hand sidebar doesn't update when a user is added to a run or playbook without a refresh.
 - If a user isn't a member of a configured broadcast channel, posting a status update might fail without any error feedback. As a temporary workaround, join the configured broadcast channels, or remove those channels from the run configuration.

### Contributors
 - [abhijit-singh](https://github.com/abhijit-singh), [agarciamontoro](https://github.com/agarciamontoro), [agnivade](https://github.com/agnivade), [alexcekay](https://github.com/alexcekay), [amyblais](https://github.com/amyblais), [andreabia](https://github.com/andreabia), [andrleite](https://github.com/andrleite), [angeloskyratzakos](https://github.com/angeloskyratzakos), [Aryakoste](https://github.com/Aryakoste), [asaadmahmood](https://github.com/asaadmahmood), [AshishDhama](https://github.com/AshishDhama), [axu-trex](https://github.com/axu-trex), [ayusht2810](https://github.com/ayusht2810), [azigler](https://github.com/azigler), [BenCookie95](https://github.com/BenCookie95), [Boruus](https://github.com/Boruus), [BrandonS09](https://github.com/BrandonS09), [bruno-keiko](https://github.com/bruno-keiko), [Camillarhi](https://github.com/Camillarhi), [catalintomai](https://github.com/catalintomai), [crspeller](https://github.com/crspeller), [ctlaltdieliet](https://translate.mattermost.com/user/ctlaltdieliet), [cwarnermm](https://github.com/cwarnermm), [danielsischy](https://github.com/danielsischy), [DemoYeti](https://github.com/DemoYeti), [devinbinnie](https://github.com/devinbinnie), [DHaussermann](https://github.com/DHaussermann), [Eleferen](https://translate.mattermost.com/user/Eleferen), [elewis787](https://github.com/elewis787), [enahum](https://github.com/enahum), [enzowritescode](https://github.com/enzowritescode), [esethna](https://github.com/esethna), [ezekielchow](https://github.com/ezekielchow), [fmartingr](https://github.com/fmartingr), [frankps](https://translate.mattermost.com/user/frankps), [gabrieljackson](https://github.com/gabrieljackson), [Gesare5](https://github.com/Gesare5), [gvarma28](https://github.com/gvarma28), [hanzei](https://github.com/hanzei), [harshilsharma63](https://github.com/harshilsharma63), [hereje](https://github.com/hereje), [hmhealey](https://github.com/hmhealey), [ifoukarakis](https://github.com/ifoukarakis), [imanmagomedov.said](https://translate.mattermost.com/user/imanmagomedov.said), [isacikgoz](https://github.com/isacikgoz), [ja49619](https://translate.mattermost.com/user/ja49619), [jasonblais](https://github.com/jasonblais), [jespino](https://github.com/jespino), [johnsonbrothers](https://github.com/johnsonbrothers), [jprusch](https://translate.mattermost.com/user/jprusch), [JulienTant](https://github.com/JulienTant), [jwilander](https://github.com/jwilander), [kaakaa](https://github.com/kaakaa), [Kshitij-Katiyar](https://github.com/Kshitij-Katiyar), [KvngMikey](https://github.com/KvngMikey), [larkox](https://github.com/larkox), [lieut-data](https://github.com/lieut-data), [lynn915](https://github.com/lynn915), [M-ZubairAhmed](https://github.com/M-ZubairAhmed), [majo](https://translate.mattermost.com/user/majo), [marianunez](https://github.com/marianunez), [master7](https://translate.mattermost.com/user/master7), [matt-w99](https://github.com/matt-w99), [matthew-w](https://translate.mattermost.com/user/matthew-w), [matthewbirtch](https://github.com/matthewbirtch), [MattSilvaa](https://github.com/MattSilvaa), [mgdelacroix](https://github.com/mgdelacroix), [movion](https://github.com/movion), [mvitale1989](https://github.com/mvitale1989), [NCPSNetworks](https://translate.mattermost.com/user/NCPSNetworks), [nickmisasi](https://github.com/nickmisasi), [ovrheat](https://github.com/ovrheat), [petersauvignon](https://translate.mattermost.com/user/petersauvignon), [phoinixgrr](https://github.com/phoinixgrr), [raghavaggarwal2308](https://github.com/raghavaggarwal2308), [rahimrahman](https://github.com/rahimrahman), [Rajat-Dabade](https://github.com/Rajat-Dabade), [RS-labhub](https://github.com/RS-labhub), [saturninoabril](https://github.com/saturninoabril), [sbishel](https://github.com/sbishel), [sblaisot](https://github.com/sblaisot), [Sn-Kinos](https://github.com/Sn-Kinos), [spirosoik](https://github.com/spirosoik), [stafot](https://github.com/stafot), [streamer45](https://github.com/streamer45), [tasnim0tantawi](https://github.com/tasnim0tantawi), [TealWater](https://github.com/TealWater), [theaino](https://github.com/theaino), [ThrRip](https://translate.mattermost.com/user/ThrRip), [Tihomir-N](https://github.com/Tihomir-N), [tnir](https://translate.mattermost.com/user/tnir), [toninis](https://github.com/toninis), [vish9812](https://github.com/vish9812), [wiggin77](https://github.com/wiggin77), [willypuzzle](https://github.com/willypuzzle), [yasserfaraazkhan](https://github.com/yasserfaraazkhan), [yomiadetutu1](https://github.com/yomiadetutu1), [ZubairImtiaz3](https://github.com/ZubairImtiaz3)
