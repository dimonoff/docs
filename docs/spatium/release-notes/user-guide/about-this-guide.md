# About this guide

## Chapters and Section Titles

The chapters correspond to the main pages in the left-hand menu of the platform (highlighted in red). The sections refer to the various options and features available within these pages.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>



**Note**: Depending on the selected license, it is possible that not all left-hand menus will be available. The “Home” and “Inventory” menus are the only two present by default on the platform. Contact your Dimonoff representative if any necessary menus do not appear.



## Solution Entities

<table data-header-hidden><thead><tr><th width="217"></th><th></th></tr></thead><tbody><tr><td>Entity</td><td>Explanation</td></tr><tr><td>Licenses</td><td>A license is an entity similar to a container. It can represent a client, a business unit, a city, a municipality, or a large group of buildings. For more information, refer to the “Project Architecture” section in the “Interface Basics” chapter.</td></tr><tr><td>Device or Asset</td><td><p>A device is an apparatus that performs a specific function in a geographic area. For example, a device can be a digital display screen, a payment kiosk, or a parking status detection sensor.<br>For more information, refer to the “Understanding the Dimonoff Parking Status Detection System” section in the “About Spatium” chapter.</p><p> </p></td></tr><tr><td>Location</td><td>A location is a geographic point within a license containing several zones. On a map, it appears as a pin defined by geographic coordinates that the user can click to enter. <br>For more information, refer to the “Project Architecture” section in the “Interface Basics” chapter.</td></tr><tr><td>Zone</td><td>A zone is a geographic area that contains several connected and/or unconnected devices. On the map, the zone appears as a shaded and enclosed area, defined by geographic coordinates and containing devices. <br>For more information, refer to the “Project Architecture” section in the “Interface Basics” chapter.</td></tr><tr><td>Group</td><td>You can group parking spots to address various management uses, such as displaying your actual sections on the parking plan, obtaining the availability of your groups or sections in a more granular manner, generating reports related to your groups, or segmenting your zones into groups to link them to panels scattered throughout your aisles. <br>For more information, refer to the “Grouping Spots” section in the “Inventory” chapter.</td></tr><tr><td>Spot</td><td>A spot is a parking location on the street or on a plan. It can be of different types such as: regular, reservation, electric vehicle, accessible, VIP, etc. Multiple spots can be linked to the same sensor: a maximum of 2 spots per MPS sensor or up to hundreds for a camera. <br>For more information, refer to the section “Configuring Parking Spots” in the “Inventory” chapter.</td></tr></tbody></table>



## Project Architecture

In the basic concepts, we saw that the highest entity in the architecture is a license. This represents a client and consists of locations. Each client can have multiple licenses.

From this, let's illustrate the project architecture in Spatium:

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

\
As a Spatium platform administrator, you can create, modify, and delete any locations and/or zones, as well as the elements within them (parking spots, access barriers, signage panels, etc.) across your various licenses.

























