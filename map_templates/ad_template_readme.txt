/====================/

Attack/Defense Gamemode Logic

/====================/

Default Gamemode Required Entities:

/====================/

logic_auto: This entity will send multiple output signals automatically.

Default Output Signals:

- OnMapSpawn - SetRedTeamRole(1) -> tf_gamerules // Set the red team as the defenders.
- OnMapSpawn - SetBlueTeamRole(2) -> tf_gamerules // Set the blue team as the attackers.
- OnMapSpawn - SetStalemateOnTimeLimit(1) // Determines whether mp_timelimit can end the match in the middle of a round.
- OnMultiNewMap - SetRedTeamRespawnWaveTime(7) // Set Respawn Times for Red Team, longer for defenders.
- OnMultiNewMap - SetBlueTeamRespawnWaveTime(2) // Set Respawn Times for Blue Team, shorter for attackers.

/====================/
filter_activator_tfteam: This entity will be used to filter out each team, used mostly for doors. There should be one for each team.

filter_activator_tfteam - filter_team_red
filter_activator_tfteam - filter_team_blue

/====================/

team_control_point_master: This entity is responsable for handling control points, in the case of Attack/Defense, it's important that Red should be restricted from winning by owning all control points.

/====================/

team_round_timer: This timer entity handles the long the setup and the round length should be. Send AddTime signals to this entity to add time on point capture.

- OnSetupTimer - relay_stage1_gates -> Trigger // When the setup timer ends, a signal is sent, this one in specific is meant to open up setup gates.
- OnTimer - game_round_win -> RoundWin // When the timer ends, a signal is sent to the game_round_win entity to declare the red team as victorious.

/====================/

game_round_win: This entity awards a victory to the team set to it, make sure that it is set to the Red team and that there's a signal to trigger a victory when the timer runs out.

/====================/

logic_relay: It's recommended that for the sake of organization, you use logic_relays for signal heavy events.

/====================/

tf_gamerules: An entity that handles games rules such as team roles, respawn times, certain HUD elements, etc.

/====================/

team_control_point: An entity that marks the location of where a capture point should be at and renders the capture point hologram. It needs to be paired with a trigger_capture_area brush entity in order to be captureable. Each point needs to have a unique name and index number.
In AD, it's important that all team control points are set to be owned by the RED team and each sequential control point should be locked behind the requirement that the previous is owned by BLUE.

/====================/

trigger_capture_area: A brush entity trigger that determines the capture area of control points. In AD, only BLUE team should be able to capture this point.

/====================/