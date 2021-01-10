# johnny_and_keith_and_some_GANs
open source fun pertaining to generative adversarial networks

using certain principles from nature to design gnarly AI

principles include:

    lateral inhibition
    
    hexagonal matrix structure a la hippocampus
    
    AIs that have like, their own wants and needs in like, a physically situated world
    
    AIs that like breed
    
    quasiautonomous networks to mimc the effcts of e.g. basal ganglia
    
    use of like ana tomical tersm, not computing terms: afferent and efferent not input and putput
    
    monsters, fires, prey
    
    singing
    
    honeycomb
    
    emotional states
    
    sight, hearing, insight
    
    aim to move from singing to discussing human psychological problems to pass the Turing Test
    
    
    like have not only a backpropagated neurl network but also a Hebbbian associative array like off to one side 
    
    
cool stuff:

    gratuitious use of the world like in all variable names, functions, code, comments and documentation
    
    TDD all the way
    
    use only Float32 numbers cos they go into GPUs better
    
    GPUs
    
    intentionally only using like lame ASCII graphics
    
    the adversarial bit is sometimes collaborative
   
   === random code sorry == long story
   
 using DataFrames
using Distances
using Gadfly

function get_how_many()
    how_many = 100
    return how_many
end

function get_near_portion()
    return 0.2
end

function get_far_portion()
    return 0.8
end

function get_Xs_Ys()
    how_many = get_how_many()
    Xs = rand(0:0.05:10, how_many)
    Ys = rand(0:0.05:10, how_many)
    return Xs, Ys
end

function build_a_circle()
    Xs, Ys = get_Xs_Ys()
    euclideans = []
    for i in 1:length(Xs)
        this_euclidean = euclidean(Xs[i], Ys[i])
        push!(euclideans, this_euclidean)
    end
    gross_points_frame = DataFrame(x=Xs, y=Ys, dist=euclideans)

    sorted_frame = sort!(gross_points_frame, [:dist])

    near_portion = get_near_portion()
    far_portion = get_far_portion()

    Xs     = sorted_frame.x
    Ys     = sorted_frame.y

    sorted_points = [collect(point) for point in zip(Xs, Ys)]

    near_point = trunc(Int64, near_portion*length(sorted_points))

    far_point = trunc(Int64, far_portion*length(sorted_points))

    keep_points = sorted_points[near_point:far_point]

    keep_Xs = [point[1] for point in keep_points]
    keep_Ys = [point[2] for point in keep_points]

    points_frame = DataFrame(x=keep_Xs, y=keep_Ys)
    return points_frame
end

function main()
    points_frame = build_a_circle()
    Xs     = points_frame.x
    Ys     = points_frame.y
    p      = plot(x=Xs, y=Ys, Geom.point)
    display(p)
end

main()

    
    
