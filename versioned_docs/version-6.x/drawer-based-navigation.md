---
id: drawer-based-navigation
title: Drawer navigation
sidebar_label: Drawer navigation
---

Common pattern in navigation is to use drawer from left (sometimes right) side for navigating between screens.

<div style={{ display: 'flex', margin: '16px 0' }}>
  <video playsInline autoPlay muted loop>
    <source src="/assets/navigators/drawer/drawer.mov" />
  </video>
</div>

Before continuing, first install [`@react-navigation/drawer`](https://github.com/react-navigation/react-navigation/tree/main/packages/drawer):

```bash npm2yarn
npm install @react-navigation/drawer
```

## Minimal example of drawer-based navigation

To use this drawer navigator, import it from `@react-navigation/drawer`:
(swipe right to open)

<samp id="drawer-based-navigation" />

```js
import * as React from 'react';
import { Button, View } from 'react-native';
import { createDrawerNavigator } from '@react-navigation/drawer';
import { NavigationContainer } from '@react-navigation/native';

function HomeScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Button
        onPress={() => navigation.navigate('Notifications')}
        title="Go to notifications"
      />
    </View>
  );
}

function NotificationsScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Button onPress={() => navigation.goBack()} title="Go back home" />
    </View>
  );
}

const Drawer = createDrawerNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Drawer.Navigator initialRouteName="Home">
        <Drawer.Screen name="Home" component={HomeScreen} />
        <Drawer.Screen name="Notifications" component={NotificationsScreen} />
      </Drawer.Navigator>
    </NavigationContainer>
  );
}
```

## Opening and closing drawer

To open and close drawer, use the following helpers:

<samp id="drawer-open-close-toggle" />

```js
navigation.openDrawer();
navigation.closeDrawer();
```

If you would like to toggle the drawer you call the following:

<samp id="drawer-open-close-toggle" />

```js
navigation.toggleDrawer();
```

Each of these functions, behind the scenes, are simply dispatching actions:

<samp id="drawer-dispatch" />

```js
navigation.dispatch(DrawerActions.openDrawer());
navigation.dispatch(DrawerActions.closeDrawer());
navigation.dispatch(DrawerActions.toggleDrawer());
```

If you would like to determine if drawer is open or closed, you can do the following:

```js
import { useDrawerStatus } from '@react-navigation/drawer';

// ...

const isDrawerOpen = useDrawerStatus() === 'open';
```
