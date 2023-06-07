# RF_NOTIFICATION_CL

This is a Dad Fedor & Swift Dungeon framework for DayZ SA.

<hr>

### Sending message from server

##### Broadcast messages
```c
void SendNotification() {
	auto notificationEntity = new RF_NOTIFICATION_NotificationEntity();
	notificationEntity.view.title.text = "PROMOCODE";
	notificationEntity.view.message.text = "Success message sent from server. (Broadcast)";
	notificationEntity.view.borderColor = RF_NOTIFICATION_Color.SUCCESS;
	RF_NOTIFICATION_SE_Global.notificationService.ShowNotification(notificationEntity);
}
```

##### Messages to concrete list of players
```c
void SendNotification(array<PlayerBase> players) {
	auto notificationEntity = new RF_NOTIFICATION_NotificationEntity();
	notificationEntity.view.title.text = "PROMOCODE";
	notificationEntity.view.message.text = "Success message sent from server. (Concrete player)";
	notificationEntity.view.borderColor = RF_NOTIFICATION_Color.SUCCESS;
	RF_NOTIFICATION_SE_Global.notificationService.ShowNotification(notificationEntity, players);
}
```

##### Messages to concrete player
```c
void SendNotification(PlayerBase player) {
	auto notificationEntity = new RF_NOTIFICATION_NotificationEntity();
	notificationEntity.view.title.text = "PROMOCODE";
	notificationEntity.view.message.text = "Success message sent from server. (Concrete player)";
	notificationEntity.view.borderColor = RF_NOTIFICATION_Color.SUCCESS;
	notificationEntity.soundSet = "RF_NOTIFICATION_CL_SoundSet1";
	RF_NOTIFICATION_SE_Global.notificationService.ShowNotification(notificationEntity, player);
}
```


### Sending message from client
```c
void SendNotification() {
	auto notificationEntity = new RF_NOTIFICATION_NotificationEntity();
	notificationEntity.view.title.text = "PROMOCODE";
	notificationEntity.view.message.text = "Error message sent from client";
	notificationEntity.view.borderColor = RF_NOTIFICATION_Color.ERROR;
	RF_NOTIFICATION_CL_Global.notificationService.ShowNotification(notificationEntity);
}
```


### Available colors (RF_NOTIFICATION_Color)
| Color   | Default Value           |
|---------|-------------------------|
| BLACK   | ARGB(122, 0, 0, 0)      |
| SUCCESS | ARGB(151, 57, 178, 0)   |
| ERROR   | ARGB(151, 255, 5, 65)   |
| WARNING | ARGB(151, 255, 199, 0)  |
| SPECIAL | ARGB(151, 191, 81, 242) |

### Available sounds (RF_NOTIFICATION_Sounds)
| Variable            | Type   | Default value                  |
|---------------------|--------|--------------------------------|
| DEFAULT_SOUND_SET_1 | string | "RF_NOTIFICATION_CL_SoundSet1" |


### Available notification configuration
| Variable | Type                    | Default value 											  |
|----------|-------------------------|------------------------------------------------------------|
| lifetime | int                     | 10            											  |
| soundSet | string       			 | RF_NOTIFICATION_Sounds.RF_NOTIFICATION_CL_SoundSet1        |
| view     | ViewConfiguration       | Object        											  |


### Available view configuration
| Variable        | Type                    | Default value                 |
|-----------------|-------------------------|-------------------------------|
| borderColor     | int                     | RF_NOTIFICATION_Color.SUCCESS |
| backgroundColor | int       				| RF_NOTIFICATION_Color.BLACK   |
| title           | string                  | ""                            |
| message         | string                  | ""                            |


### Text configuration
| Variable | Type   | Default value                 |
|----------|--------|-------------------------------|
| color    | int    | RF_NOTIFICATION_Color.SUCCESS |
| text     | string | ""                            |


</br><hr></br>


### Additional info
```c

// To Concrete player
string notificationEntityString = getNotificationEntity(lifetime, title, titleColor, message, messageColor, borderColor, backgroundColor);
auto mission = GetGame().GetMission();
GetGame().GameScript.CallFunctionParams(mission, "RF_NOTIFICATION_SE_ShowNotificationToPlayer", NULL, new Param2<string, PlayerBase>(notificationEntityString, players);


// To Players
string notificationEntityString = getNotificationEntity(lifetime, title, titleColor, message, messageColor, borderColor, backgroundColor);
auto mission = GetGame().GetMission();
GetGame().GameScript.CallFunctionParams(mission, "RF_NOTIFICATION_SE_ShowNotificationToPlayers", NULL, new Param2<string, array<PlayerBase>>(notificationEntityString, players));


// From client
string notificationEntityString = getNotificationEntity(lifetime, title, titleColor, message, messageColor, borderColor, backgroundColor);
auto mission = MissionGameplay.Cast(GetGame().GetMission());
GetGame().GameScript.CallFunctionParams(mission, "RF_NOTIFICATION_CL_ShowNotification", NULL, new Param1<string>(notificationEntityString));

private string getNotificationEntity(
	int lifetime,
	string title, 
	int titleColor,
	string message, 
	int messageColor,
	int borderColor,
	int backgroundColor
) {
	string soundSet = "RF_NOTIFICATION_CL_SoundSet1";
	string titleConfig = string.Format("{\"text\": \"%1\", \"color\": %2}", title, titleColor);
	string messageConfig = string.Format("{\"text\": \"%1\",\"color\": %2}", message, messageColor);
	string viewConfiguration = string.Format("{\"title\": %1,\"message\": %2,\"borderColor\": %3,\"backgroundColor\": %4}", titleConfig, messageConfig, borderColor, backgroundColor);
	return string.Format("{\"lifetime\": %1, \"soundSet\": \"%2\", \"view\": %3}", lifetime, soundSet, viewConfiguration);
}

private bool RF_NOTIFICATION_isDefined() {
	auto modString = "RF_NOTIFICATION_CL";
    if (!modString.ToType()) return false;
    return true;
}
```

</br><hr></br>

## Contributors

* [romabeorn](https://github.com/romabeorn)
* [Patison5](https://github.com/Patison5)
