SDA Tracking API - Go
================================
Use Go to track SDA shipments with SDA Tracking API.

Features
--------
- Real-time SDA tracking.
- Batch SDA tracking.
- Other features to manage your SDA tracking.

Installation
------------

Installation is easy:

    $ go mod init github.com/my/repo
    $ go get github.com/trackingmore-api/trackingmore-sdk-go

Quick Start
----------
Get the API key:

To use this API, you need to generate your API key.

- <a href="https://admin.trackingmore.com/developer/apikey" target="_blank" rel="noreferrer">
  Click here</a> to access TrackingMore admin.

- Go to the "Developer" section.

- Click "Generate API Key".

- Give a name to your API key, and click "Save" .


Then, start to track your SDA shipments.

Usage
----------

Create a tracking (Real-time tracking):

    package main

    import (
      "context"
      "fmt"
      "github.com/trackingmore-api/trackingmore-sdk-go"
    )
    
    func main() {
      key := "your api key"
      cli, err := trackingmore.NewClient(key)
      
      if err != nil {
        fmt.Println(err)
        return
      }
      
      params := trackingmore.CreateTrackingParams{
        TrackingNumber: "3UW19XY000127",
        CourierCode:    "italy-sda",
      }      

      result, err := cli.CreateTracking(context.Background(), params)
      if err != nil {
        fmt.Println(err)
        return
      }
      
      fmt.Println(result)
    }


Create trackings (Max. 40 tracking numbers create in one call):

    package main

    import (
      "context"
      "fmt"
      "github.com/trackingmore-api/trackingmore-sdk-go"
    )
    
    func main() {
      key := "your api key"
      cli, err := trackingmore.NewClient(key)
      
      if err != nil {
        fmt.Println(err)
        return
      }
      
      params := []trackingmore.CreateTrackingParams{
          {
          TrackingNumber: "4UW1CEG000511",
          CourierCode:    "italy-sda",
          },
          {
          TrackingNumber: "3UW0H2H018366",
          CourierCode:    "italy-sda",
          },
      }   

      result, err := cli.BatchCreateTrackings(context.Background(), params)
      if err != nil {
        fmt.Println(err)
        return
      }
      
      fmt.Println(result)
    }


Get status of the shipment:

    package main

    import (
      "context"
      "fmt"
      "github.com/trackingmore-api/trackingmore-sdk-go"
    )
    
    func main() {
      key := "your api key"
      cli, err := trackingmore.NewClient(key)
      
      if err != nil {
        fmt.Println(err)
        return
      }

      params := trackingmore.GetTrackingResultsParams{
        CreatedDateMin: "2023-08-23T06:00:00+00:00",
        CreatedDateMax: "2023-09-05T07:20:42+00:00",
      }  

      result, err := cli.GetTrackingResults(context.Background(), params)
      if err != nil {
        fmt.Println(err)
        return
      }
      
      fmt.Println(result)
    }


Update a tracking by ID:

    package main

    import (
      "context"
      "fmt"
      "github.com/trackingmore-api/trackingmore-sdk-go"
    )
    
    func main() {
      key := "your api key"
      cli, err := trackingmore.NewClient(key)
      
      if err != nil {
        fmt.Println(err)
        return
      }

      params := trackingmore.UpdateTrackingParams{
        CustomerName: "New name",
        Note:         "New tests order note",
      }
      idString := "9bffeedce4fe07569bb9df29f12a919e"
      
      result, err := cli.UpdateTrackingByID(context.Background(), idString, params)
      if err != nil {
        fmt.Println(err)
        return
      }
      
      fmt.Println(result)
    }
