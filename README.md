# Extracting a Service Class

## Learning Goals

- 
## Introduction

In the previous lessons, we started to see how customizing our JSON data in the
controller works, but can start to get pretty complicated. It is possible for
a single controller action to render data from multiple models on our Rails
API. It is also possible to specify what we want and don't want to render. 

The complication comes when we start to scale. More models, more data, more
pieces to customize until it becomes unmanageable. In this lesson, we're going
to look at building our own solution to this problem.

## Initial Configuration

The files in this lesson were populated using the API-only Rails build for you
to code along. There are already three resources set up based on where we left
off in the previous lesson on `include`: birds, locations, and sightings. Birds
and locations are related together through sightings:

```rb
class Bird < ApplicationRecord
    has_many :sightings
    has_many :locations, through: :sightings
end
```

```rb
class Location < ApplicationRecord
    has_many :sightings
    has_many :birds, through: :sightings
end
```

```rb
class Sighting < ApplicationRecord
  belongs_to :bird
  belongs_to :location
end
```

And we left off with a complicated mess of `include`, `only` and `except` in
order to customize what attributes we wanted to render to JSON:

```rb
class SightingsController < ApplicationController
  def show
    @sighting = Sighting.find(params[:id])
    render json: @sighting.to_json(:include => {:bird => {:only =>[:name, :species]}, :location => {:only =>[:latitude, :longitude]}}, :except => [:updated_at])
  end
end
```

This presents some problems. For one, this is only _one_ action. Are we going to need to do this for every controller action? 

## SWBAT 1

## SWBAT 2

## Conclusion

## Resources
